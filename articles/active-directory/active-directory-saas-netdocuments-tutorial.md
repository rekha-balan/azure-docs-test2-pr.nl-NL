---
title: 'Tutorial: Azure Active Directory integration with NetDocuments | Microsoft Docs'
description: Learn how to use NetDocuments with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: 7162dc3daea0f454423868ac2e23f055e7d48683
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552707"
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="f51b2-103">Tutorial: Azure Active Directory integration with NetDocuments</span><span class="sxs-lookup"><span data-stu-id="f51b2-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>
<span data-ttu-id="f51b2-104">The objective of this tutorial is to show the integration of Azure and NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="f51b2-104">The objective of this tutorial is to show the integration of Azure and NetDocuments.</span></span> <span data-ttu-id="f51b2-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="f51b2-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="f51b2-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="f51b2-106">A valid Azure subscription</span></span>
* <span data-ttu-id="f51b2-107">A NetDocuments tenant</span><span class="sxs-lookup"><span data-stu-id="f51b2-107">A NetDocuments tenant</span></span>

<span data-ttu-id="f51b2-108">After completing this tutorial, the Azure AD users you have assigned to NetDocuments will be able to single sign into the application at your NetDocuments company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f51b2-108">After completing this tutorial, the Azure AD users you have assigned to NetDocuments will be able to single sign into the application at your NetDocuments company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="f51b2-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f51b2-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="f51b2-110">Enabling the application integration for NetDocuments</span><span class="sxs-lookup"><span data-stu-id="f51b2-110">Enabling the application integration for NetDocuments</span></span>
2. <span data-ttu-id="f51b2-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="f51b2-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="f51b2-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="f51b2-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="f51b2-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="f51b2-113">Assigning users</span></span>

<span data-ttu-id="f51b2-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795040.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="f51b2-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795040.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-netdocuments"></a><span data-ttu-id="f51b2-115">Enabling the application integration for NetDocuments</span><span class="sxs-lookup"><span data-stu-id="f51b2-115">Enabling the application integration for NetDocuments</span></span>
<span data-ttu-id="f51b2-116">The objective of this section is to outline how to enable the application integration for NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="f51b2-116">The objective of this section is to outline how to enable the application integration for NetDocuments.</span></span>

<span data-ttu-id="f51b2-117">**To enable the application integration for NetDocuments, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f51b2-117">**To enable the application integration for NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="f51b2-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f51b2-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="f51b2-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="f51b2-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="f51b2-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="f51b2-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="f51b2-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="f51b2-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="f51b2-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="f51b2-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="f51b2-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="f51b2-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="f51b2-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="f51b2-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="f51b2-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="f51b2-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="f51b2-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="f51b2-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="f51b2-127">In the **search box**, type **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="f51b2-127">In the **search box**, type **NetDocuments**.</span></span>
   
   <span data-ttu-id="f51b2-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795041.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="f51b2-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795041.png "Application Gallery")</span></span>
7. <span data-ttu-id="f51b2-129">In the results pane, select **NetDocuments**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="f51b2-129">In the results pane, select **NetDocuments**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="f51b2-130">![NetDocuments](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795042.png "NetDocuments")</span><span class="sxs-lookup"><span data-stu-id="f51b2-130">![NetDocuments](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795042.png "NetDocuments")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="f51b2-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="f51b2-131">Configure single sign-on</span></span>

<span data-ttu-id="f51b2-132">The objective of this section is to outline how to enable users to authenticate to NetDocuments with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="f51b2-132">The objective of this section is to outline how to enable users to authenticate to NetDocuments with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="f51b2-133">Configuring SSO for NetDocuments requires you to retrieve a thumbprint value from a certificate.</span><span class="sxs-lookup"><span data-stu-id="f51b2-133">Configuring SSO for NetDocuments requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="f51b2-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="f51b2-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="f51b2-135">**To configure SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f51b2-135">**To configure SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="f51b2-136">In the Azure classic portal, on the **NetDocuments** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="f51b2-136">In the Azure classic portal, on the **NetDocuments** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="f51b2-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795043.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f51b2-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795043.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="f51b2-138">On the **How would you like users to sign on to NetDocuments** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f51b2-138">On the **How would you like users to sign on to NetDocuments** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="f51b2-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795044.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f51b2-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795044.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="f51b2-140">On the **Configure App URL** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f51b2-140">On the **Configure App URL** page, perform the following steps:</span></span>
   
   <span data-ttu-id="f51b2-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795045.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="f51b2-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795045.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="f51b2-142">In the **Sign On URL** textbox, type your URL used by your users to sign on to your NetDocuments application (e.g.: "*https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=CA-JI1BG3H1*").</span><span class="sxs-lookup"><span data-stu-id="f51b2-142">In the **Sign On URL** textbox, type your URL used by your users to sign on to your NetDocuments application (e.g.: "*https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=CA-JI1BG3H1*").</span></span>
   2. <span data-ttu-id="f51b2-143">In the **NetDocuments Reply URL** textbox, type the same value you have typed into the the **Sign On URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f51b2-143">In the **NetDocuments Reply URL** textbox, type the same value you have typed into the the **Sign On URL** textbox.</span></span>  
      
      >[!NOTE]
      ><span data-ttu-id="f51b2-144">You can find the correct value at the end of the **Federated Identity** dialog (See the screenshot for step 9).</span><span class="sxs-lookup"><span data-stu-id="f51b2-144">You can find the correct value at the end of the **Federated Identity** dialog (See the screenshot for step 9).</span></span>
      >
      >
     
   3. <span data-ttu-id="f51b2-145">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f51b2-145">Click **Next**.</span></span>
4. <span data-ttu-id="f51b2-146">On the **Configure single sign-on at NetDocuments** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="f51b2-146">On the **Configure single sign-on at NetDocuments** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
   <span data-ttu-id="f51b2-147">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795046.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f51b2-147">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795046.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="f51b2-148">In a different web browser window, log into your NetDocuments company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f51b2-148">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>
6. <span data-ttu-id="f51b2-149">Go to **Admin**.</span><span class="sxs-lookup"><span data-stu-id="f51b2-149">Go to **Admin**.</span></span>
7. <span data-ttu-id="f51b2-150">Click **Add and remove users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f51b2-150">Click **Add and remove users and groups**.</span></span>
   
   <span data-ttu-id="f51b2-151">![Repository](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795047.png "Repository")</span><span class="sxs-lookup"><span data-stu-id="f51b2-151">![Repository](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795047.png "Repository")</span></span>
8. <span data-ttu-id="f51b2-152">Click **Configure advanced authentication options**.</span><span class="sxs-lookup"><span data-stu-id="f51b2-152">Click **Configure advanced authentication options**.</span></span>
   
   <span data-ttu-id="f51b2-153">![Configure advanced authentication options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795048.png "Configure advanced authentication options")</span><span class="sxs-lookup"><span data-stu-id="f51b2-153">![Configure advanced authentication options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795048.png "Configure advanced authentication options")</span></span>
9. <span data-ttu-id="f51b2-154">On **the Federated Identity** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f51b2-154">On **the Federated Identity** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="f51b2-155">![Federated Identitty](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795049.png "Federated Identitty")</span><span class="sxs-lookup"><span data-stu-id="f51b2-155">![Federated Identitty](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795049.png "Federated Identitty")</span></span>
   
   1. <span data-ttu-id="f51b2-156">As **Federated identity server type**, select **Active Directory Federation Services**.</span><span class="sxs-lookup"><span data-stu-id="f51b2-156">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   2. <span data-ttu-id="f51b2-157">Click **Choose file**, to upload the downloaded metadata file.</span><span class="sxs-lookup"><span data-stu-id="f51b2-157">Click **Choose file**, to upload the downloaded metadata file.</span></span>
   3. <span data-ttu-id="f51b2-158">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f51b2-158">Click **OK**.</span></span>
10. <span data-ttu-id="f51b2-159">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="f51b2-159">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="f51b2-160">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795050.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f51b2-160">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795050.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="f51b2-161">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="f51b2-161">Configure user provisioning</span></span>

<span data-ttu-id="f51b2-162">In order to enable Azure AD users to log into NetDocuments, they must be provisioned into NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="f51b2-162">In order to enable Azure AD users to log into NetDocuments, they must be provisioned into NetDocuments.</span></span> <span data-ttu-id="f51b2-163">In the case of NetDocuments, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="f51b2-163">In the case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="f51b2-164">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f51b2-164">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="f51b2-165">Sing on to your **NetDocuments** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="f51b2-165">Sing on to your **NetDocuments** company site as administrator.</span></span>
2. <span data-ttu-id="f51b2-166">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="f51b2-166">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="f51b2-167">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795051.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="f51b2-167">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795051.png "Admin")</span></span>
3. <span data-ttu-id="f51b2-168">Click **Add and remove users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f51b2-168">Click **Add and remove users and groups**.</span></span>
   
   <span data-ttu-id="f51b2-169">![Repository](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795047.png "Repository")</span><span class="sxs-lookup"><span data-stu-id="f51b2-169">![Repository](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795047.png "Repository")</span></span>
4. <span data-ttu-id="f51b2-170">In the **Email Address** textbox, type the email address of a valid Azure Active Directory account you want to provision, and then click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="f51b2-170">In the **Email Address** textbox, type the email address of a valid Azure Active Directory account you want to provision, and then click **Add User**.</span></span>
   
   <span data-ttu-id="f51b2-171">![Email Address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795053.png "Email Address")</span><span class="sxs-lookup"><span data-stu-id="f51b2-171">![Email Address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="f51b2-172">The Azure Active Directory account holder will get an email that includes a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="f51b2-172">The Azure Active Directory account holder will get an email that includes a link to confirm the account before it becomes active.</span></span>
   > 
   > 

>[!NOTE]
><span data-ttu-id="f51b2-173">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="f51b2-173">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments to provision AAD user accounts.</span></span>
>
>

## <a name="assign-users"></a><span data-ttu-id="f51b2-174">Assign users</span><span class="sxs-lookup"><span data-stu-id="f51b2-174">Assign users</span></span>
<span data-ttu-id="f51b2-175">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="f51b2-175">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="f51b2-176">**To assign users to NetDocuments, perform the following steps;**</span><span class="sxs-lookup"><span data-stu-id="f51b2-176">**To assign users to NetDocuments, perform the following steps;**</span></span>

1. <span data-ttu-id="f51b2-177">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="f51b2-177">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="f51b2-178">On the \*\*NetDocuments \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="f51b2-178">On the \*\*NetDocuments \*\*application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="f51b2-179">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795054.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="f51b2-179">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795054.png "Assign Users")</span></span>
3. <span data-ttu-id="f51b2-180">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="f51b2-180">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="f51b2-181">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="f51b2-181">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="f51b2-182">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f51b2-182">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="f51b2-183">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f51b2-183">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f51b2-184">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f51b2-184">Additional resources</span></span>

* [<span data-ttu-id="f51b2-185">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f51b2-185">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f51b2-186">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f51b2-186">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



















