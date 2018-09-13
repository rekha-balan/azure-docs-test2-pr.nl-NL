---
title: 'Tutorial: Azure Active Directory integration with Innotas | Microsoft Docs'
description: Learn how to use Innotas with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: eb9e9c2c-4b09-4177-bbab-423fd657448e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/02/2017
ms.author: jeedes
ms.openlocfilehash: 4b3b0e7998542aa8abe73422217ab116def303cc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551818"
---
# <a name="tutorial-azure-active-directory-integration-with-innotas"></a><span data-ttu-id="c8828-103">Tutorial: Azure Active Directory integration with Innotas</span><span class="sxs-lookup"><span data-stu-id="c8828-103">Tutorial: Azure Active Directory integration with Innotas</span></span>
<span data-ttu-id="c8828-104">The objective of this tutorial is to show the integration of Azure and Innotas.</span><span class="sxs-lookup"><span data-stu-id="c8828-104">The objective of this tutorial is to show the integration of Azure and Innotas.</span></span>  
<span data-ttu-id="c8828-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="c8828-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="c8828-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="c8828-106">A valid Azure subscription</span></span>
* <span data-ttu-id="c8828-107">A Innotas tenant</span><span class="sxs-lookup"><span data-stu-id="c8828-107">A Innotas tenant</span></span>

<span data-ttu-id="c8828-108">After completing this tutorial, the Azure AD users you have assigned to Innotas will be able to single sign into the application at your Innotas company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8828-108">After completing this tutorial, the Azure AD users you have assigned to Innotas will be able to single sign into the application at your Innotas company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="c8828-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c8828-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="c8828-110">Enabling the application integration for Innotas</span><span class="sxs-lookup"><span data-stu-id="c8828-110">Enabling the application integration for Innotas</span></span>
* <span data-ttu-id="c8828-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="c8828-111">Configuring single sign-on</span></span>
* <span data-ttu-id="c8828-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="c8828-112">Configuring user provisioning</span></span>
*  <span data-ttu-id="c8828-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="c8828-113">Assigning users</span></span>

<span data-ttu-id="c8828-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777331.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="c8828-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777331.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-innotas"></a><span data-ttu-id="c8828-115">Enable the application integration for Innotas</span><span class="sxs-lookup"><span data-stu-id="c8828-115">Enable the application integration for Innotas</span></span>
<span data-ttu-id="c8828-116">The objective of this section is to outline how to enable the application integration for Innotas.</span><span class="sxs-lookup"><span data-stu-id="c8828-116">The objective of this section is to outline how to enable the application integration for Innotas.</span></span>

<span data-ttu-id="c8828-117">**To enable the application integration for Innotas, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c8828-117">**To enable the application integration for Innotas, perform the following steps:**</span></span>

1. <span data-ttu-id="c8828-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c8828-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="c8828-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="c8828-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="c8828-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c8828-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c8828-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c8828-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="c8828-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="c8828-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="c8828-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="c8828-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="c8828-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="c8828-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="c8828-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="c8828-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="c8828-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="c8828-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="c8828-127">In the **search box**, type **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="c8828-127">In the **search box**, type **Innotas**.</span></span>
   
   <span data-ttu-id="c8828-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777332.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="c8828-128">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777332.png "Application gallery")</span></span>
7. <span data-ttu-id="c8828-129">In the results pane, select **Innotas**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="c8828-129">In the results pane, select **Innotas**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="c8828-130">![Innotas](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777333.png "Innotas")</span><span class="sxs-lookup"><span data-stu-id="c8828-130">![Innotas](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777333.png "Innotas")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="c8828-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="c8828-131">Configure single sign-on</span></span>

<span data-ttu-id="c8828-132">The objective of this section is to outline how to enable users to authenticate to Innotas with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="c8828-132">The objective of this section is to outline how to enable users to authenticate to Innotas with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="c8828-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c8828-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="c8828-134">In the Azure classic portal, on the **Innotas** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="c8828-134">In the Azure classic portal, on the **Innotas** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="c8828-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777334.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c8828-135">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777334.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="c8828-136">On the **How would you like users to sign on to Innotas** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c8828-136">On the **How would you like users to sign on to Innotas** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="c8828-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777335.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c8828-137">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777335.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="c8828-138">On the **Configure App URL** page, in the **Innotas Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.Innotas.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c8828-138">On the **Configure App URL** page, in the **Innotas Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.Innotas.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="c8828-139">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777336.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="c8828-139">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777336.png "Configure app URL")</span></span>
4. <span data-ttu-id="c8828-140">On the **Configure single sign-on at Innotas** page, to download your metadata, click **Download metadata**, and then the data file locally as **c:\\InnotasMetaData.xml**.</span><span class="sxs-lookup"><span data-stu-id="c8828-140">On the **Configure single sign-on at Innotas** page, to download your metadata, click **Download metadata**, and then the data file locally as **c:\\InnotasMetaData.xml**.</span></span>
   
   <span data-ttu-id="c8828-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777337.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c8828-141">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777337.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="c8828-142">Forward that metadata file to Innotas support team.</span><span class="sxs-lookup"><span data-stu-id="c8828-142">Forward that metadata file to Innotas support team.</span></span> <span data-ttu-id="c8828-143">The support team needs configures single sign-on for you.</span><span class="sxs-lookup"><span data-stu-id="c8828-143">The support team needs configures single sign-on for you.</span></span>
6. <span data-ttu-id="c8828-144">Select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="c8828-144">Select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="c8828-145">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777338.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="c8828-145">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777338.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="c8828-146">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="c8828-146">Configure user provisioning</span></span>

<span data-ttu-id="c8828-147">There is no action item for you to configure user provisioning to Innotas.</span><span class="sxs-lookup"><span data-stu-id="c8828-147">There is no action item for you to configure user provisioning to Innotas.</span></span>  
<span data-ttu-id="c8828-148">When an assigned user tries to log into Innotas using the access panel, Innotas checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="c8828-148">When an assigned user tries to log into Innotas using the access panel, Innotas checks whether the user exists.</span></span>  

>[!NOTE]
><span data-ttu-id="c8828-149">If there is no user account available yet, it is automatically created by Innotas.</span><span class="sxs-lookup"><span data-stu-id="c8828-149">If there is no user account available yet, it is automatically created by Innotas.</span></span>
>

## <a name="assign-users"></a><span data-ttu-id="c8828-150">Assign users</span><span class="sxs-lookup"><span data-stu-id="c8828-150">Assign users</span></span>
<span data-ttu-id="c8828-151">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="c8828-151">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="c8828-152">**To assign users to Innotas, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c8828-152">**To assign users to Innotas, perform the following steps:**</span></span>

1. <span data-ttu-id="c8828-153">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="c8828-153">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="c8828-154">On the **Innotas** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="c8828-154">On the **Innotas** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="c8828-155">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777339.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="c8828-155">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC777339.png "Assign users")</span></span>
3. <span data-ttu-id="c8828-156">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="c8828-156">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="c8828-157">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="c8828-157">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-innotas-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="c8828-158">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c8828-158">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="c8828-159">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8828-159">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>















