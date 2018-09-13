---
title: 'Tutorial: Azure Active Directory Integration with ArcGIS | Microsoft Docs'
description: Learn how to use ArcGIS with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 718373a95f12de04c710bb0dc81c2d3138786902
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551076"
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis"></a><span data-ttu-id="ca631-103">Tutorial: Azure Active Directory Integration with ArcGIS</span><span class="sxs-lookup"><span data-stu-id="ca631-103">Tutorial: Azure Active Directory Integration with ArcGIS</span></span>
<span data-ttu-id="ca631-104">The objective of this tutorial is to show the integration of Azure and ArcGIS.</span><span class="sxs-lookup"><span data-stu-id="ca631-104">The objective of this tutorial is to show the integration of Azure and ArcGIS.</span></span> <span data-ttu-id="ca631-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="ca631-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="ca631-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="ca631-106">A valid Azure subscription</span></span>
* <span data-ttu-id="ca631-107">An ArcGIS single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ca631-107">An ArcGIS single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="ca631-108">After completing this tutorial, the Azure AD users you have assigned to ArcGIS will be able to single sign into the application at your ArcGIS company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ca631-108">After completing this tutorial, the Azure AD users you have assigned to ArcGIS will be able to single sign into the application at your ArcGIS company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="ca631-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ca631-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="ca631-110">Enabling the application integration for ArcGIS</span><span class="sxs-lookup"><span data-stu-id="ca631-110">Enabling the application integration for ArcGIS</span></span>
* <span data-ttu-id="ca631-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="ca631-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="ca631-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="ca631-112">Configuring user provisioning</span></span>
* <span data-ttu-id="ca631-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="ca631-113">Assigning users</span></span>

<span data-ttu-id="ca631-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784735.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="ca631-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784735.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-arcgis"></a><span data-ttu-id="ca631-115">Enable the application integration for ArcGIS</span><span class="sxs-lookup"><span data-stu-id="ca631-115">Enable the application integration for ArcGIS</span></span>
<span data-ttu-id="ca631-116">The objective of this section is to outline how to enable the application integration for ArcGIS.</span><span class="sxs-lookup"><span data-stu-id="ca631-116">The objective of this section is to outline how to enable the application integration for ArcGIS.</span></span>

<span data-ttu-id="ca631-117">**To enable the application integration for ArcGIS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ca631-117">**To enable the application integration for ArcGIS, perform the following steps:**</span></span>

1. <span data-ttu-id="ca631-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ca631-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="ca631-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="ca631-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="ca631-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="ca631-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ca631-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="ca631-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="ca631-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="ca631-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="ca631-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="ca631-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="ca631-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="ca631-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="ca631-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="ca631-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="ca631-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="ca631-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="ca631-127">In the **search box**, type **ArcGIS**.</span><span class="sxs-lookup"><span data-stu-id="ca631-127">In the **search box**, type **ArcGIS**.</span></span>
   
   <span data-ttu-id="ca631-128">![Applcation Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784736.png "Applcation Gallery")</span><span class="sxs-lookup"><span data-stu-id="ca631-128">![Applcation Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784736.png "Applcation Gallery")</span></span>
7. <span data-ttu-id="ca631-129">In the results pane, select **ArcGIS**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="ca631-129">In the results pane, select **ArcGIS**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="ca631-130">![ArcGIS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784737.png "ArcGIS")</span><span class="sxs-lookup"><span data-stu-id="ca631-130">![ArcGIS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784737.png "ArcGIS")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="ca631-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="ca631-131">Configure single sign-on</span></span>

<span data-ttu-id="ca631-132">The objective of this section is to outline how to enable users to authenticate to ArcGIS with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="ca631-132">The objective of this section is to outline how to enable users to authenticate to ArcGIS with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="ca631-133">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ca631-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="ca631-134">In the Azure classic portal, on the **ArcGIS** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="ca631-134">In the Azure classic portal, on the **ArcGIS** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="ca631-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784738.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ca631-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784738.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="ca631-136">On the **How would you like users to sign on to ArcGIS** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ca631-136">On the **How would you like users to sign on to ArcGIS** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="ca631-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784739.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ca631-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784739.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="ca631-138">On the **Configure App URL** page, in the **ArcGIS Sign In URL** textbox, type the URL used by your users to sign in using the following pattern "*https://company.maps.arcgis.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ca631-138">On the **Configure App URL** page, in the **ArcGIS Sign In URL** textbox, type the URL used by your users to sign in using the following pattern "*https://company.maps.arcgis.com*", and then click **Next**.</span></span>
   
   <span data-ttu-id="ca631-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784740.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="ca631-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784740.png "Configure App URL")</span></span>
4. <span data-ttu-id="ca631-140">On the **Configure single sign-on at ArcGIS** page, click **Download metadata**, and then save the metadata file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="ca631-140">On the **Configure single sign-on at ArcGIS** page, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="ca631-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784741.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ca631-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784741.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="ca631-142">In a different web browser window, log into your ArcGIS company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ca631-142">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>
6. <span data-ttu-id="ca631-143">Click **Edit Settings**.</span><span class="sxs-lookup"><span data-stu-id="ca631-143">Click **Edit Settings**.</span></span>
   
   <span data-ttu-id="ca631-144">![Edit Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784742.png "Edit Settings")</span><span class="sxs-lookup"><span data-stu-id="ca631-144">![Edit Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784742.png "Edit Settings")</span></span>
7. <span data-ttu-id="ca631-145">Click **Security**.</span><span class="sxs-lookup"><span data-stu-id="ca631-145">Click **Security**.</span></span>
   
   <span data-ttu-id="ca631-146">![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784743.png "Security")</span><span class="sxs-lookup"><span data-stu-id="ca631-146">![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784743.png "Security")</span></span>
8. <span data-ttu-id="ca631-147">Under **Enterprise Logins**, click **Set Identity Provider**.</span><span class="sxs-lookup"><span data-stu-id="ca631-147">Under **Enterprise Logins**, click **Set Identity Provider**.</span></span>
   
   <span data-ttu-id="ca631-148">![Enterprise Logins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784744.png "Enterprise Logins")</span><span class="sxs-lookup"><span data-stu-id="ca631-148">![Enterprise Logins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784744.png "Enterprise Logins")</span></span>
9. <span data-ttu-id="ca631-149">On the **Set Identity Provider** configuration page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ca631-149">On the **Set Identity Provider** configuration page, perform the following steps:</span></span>
   
   <span data-ttu-id="ca631-150">![Set Identity Provider](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784745.png "Set Identity Provider")</span><span class="sxs-lookup"><span data-stu-id="ca631-150">![Set Identity Provider](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784745.png "Set Identity Provider")</span></span>
   
   1. <span data-ttu-id="ca631-151">In the Name textbox, type your organization’s name.</span><span class="sxs-lookup"><span data-stu-id="ca631-151">In the Name textbox, type your organization’s name.</span></span>
   2. <span data-ttu-id="ca631-152">For **Metadata for the Enterprise Identity Provider will be supplied using**, select **A File**.</span><span class="sxs-lookup"><span data-stu-id="ca631-152">For **Metadata for the Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>
   3. <span data-ttu-id="ca631-153">To upload your downloaded metadata file, click **Choose file**.</span><span class="sxs-lookup"><span data-stu-id="ca631-153">To upload your downloaded metadata file, click **Choose file**.</span></span>
   4. <span data-ttu-id="ca631-154">Click **Set Identity Provider**.</span><span class="sxs-lookup"><span data-stu-id="ca631-154">Click **Set Identity Provider**.</span></span>
10. <span data-ttu-id="ca631-155">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="ca631-155">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="ca631-156">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784746.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ca631-156">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784746.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="ca631-157">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="ca631-157">Configure user provisioning</span></span>

<span data-ttu-id="ca631-158">In order to enable Azure AD users to log into ArcGIS, they must be provisioned into ArcGIS.</span><span class="sxs-lookup"><span data-stu-id="ca631-158">In order to enable Azure AD users to log into ArcGIS, they must be provisioned into ArcGIS.</span></span>

* <span data-ttu-id="ca631-159">In the case of ArcGIS, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="ca631-159">In the case of ArcGIS, provisioning is a manual task.</span></span>

<span data-ttu-id="ca631-160">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ca631-160">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="ca631-161">Log in to your **ArcGIS** tenant.</span><span class="sxs-lookup"><span data-stu-id="ca631-161">Log in to your **ArcGIS** tenant.</span></span>
2. <span data-ttu-id="ca631-162">Click **Invite Members**.</span><span class="sxs-lookup"><span data-stu-id="ca631-162">Click **Invite Members**.</span></span>
   
   <span data-ttu-id="ca631-163">![Invite Members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784747.png "Invite Members")</span><span class="sxs-lookup"><span data-stu-id="ca631-163">![Invite Members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784747.png "Invite Members")</span></span>
3. <span data-ttu-id="ca631-164">Select **Add members automatically without sending an email**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ca631-164">Select **Add members automatically without sending an email**, and then click **Next**.</span></span>
   
   <span data-ttu-id="ca631-165">![Add Members Automatically](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784748.png "Add Members Automatically")</span><span class="sxs-lookup"><span data-stu-id="ca631-165">![Add Members Automatically](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784748.png "Add Members Automatically")</span></span>
4. <span data-ttu-id="ca631-166">On the **Members** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ca631-166">On the **Members** dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="ca631-167">![Add and review](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784749.png "Add and review")</span><span class="sxs-lookup"><span data-stu-id="ca631-167">![Add and review](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784749.png "Add and review")</span></span>
   1. <span data-ttu-id="ca631-168">Enter the **First Name**, **Last Name** and **Email** of a valid AAD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="ca631-168">Enter the **First Name**, **Last Name** and **Email** of a valid AAD account you want to provision.</span></span>
   2. <span data-ttu-id="ca631-169">Click **Add And Review**.</span><span class="sxs-lookup"><span data-stu-id="ca631-169">Click **Add And Review**.</span></span>
5. <span data-ttu-id="ca631-170">Review the data you have entered, and then click **Add Members**.</span><span class="sxs-lookup"><span data-stu-id="ca631-170">Review the data you have entered, and then click **Add Members**.</span></span>
   
   <span data-ttu-id="ca631-171">![Add member](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784750.png "Add member")</span><span class="sxs-lookup"><span data-stu-id="ca631-171">![Add member](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784750.png "Add member")</span></span>

>[!NOTE]
><span data-ttu-id="ca631-172">You can use any other ArcGIS user account creation tools or APIs provided by ArcGIS to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="ca631-172">You can use any other ArcGIS user account creation tools or APIs provided by ArcGIS to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="ca631-173">Assign users</span><span class="sxs-lookup"><span data-stu-id="ca631-173">Assign users</span></span>
<span data-ttu-id="ca631-174">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="ca631-174">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="ca631-175">**To assign users to ArcGIS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ca631-175">**To assign users to ArcGIS, perform the following steps:**</span></span>
1. <span data-ttu-id="ca631-176">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="ca631-176">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="ca631-177">On the \*\*ArcGIS \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="ca631-177">On the \*\*ArcGIS \*\*application integration page, click **Assign users**.</span></span>
   
  <span data-ttu-id="ca631-178">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784751.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="ca631-178">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC784751.png "Assign Users")</span></span>
3. <span data-ttu-id="ca631-179">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="ca631-179">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
  <span data-ttu-id="ca631-180">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="ca631-180">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-arcgis-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="ca631-181">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ca631-181">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="ca631-182">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ca631-182">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>























