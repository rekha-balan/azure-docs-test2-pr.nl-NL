---
title: 'Tutorial: Azure Active Directory integration with HR2day by Merces | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and HR2day by Merces.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 984e2e9999a2aba7a595034f1fec8bafb976f310
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871301"
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="05868-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span><span class="sxs-lookup"><span data-stu-id="05868-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="05868-104">In this tutorial, you learn how to integrate HR2day by Merces with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05868-104">In this tutorial, you learn how to integrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="05868-105">Integrating HR2day by Merces with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="05868-105">Integrating HR2day by Merces with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="05868-106">You can control in Azure AD who has access to HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="05868-106">You can control in Azure AD who has access to HR2day by Merces.</span></span>
- <span data-ttu-id="05868-107">You can enable your users to automatically get signed in to HR2day by Merces with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="05868-107">You can enable your users to automatically get signed in to HR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="05868-108">You can manage your accounts in one central location--the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="05868-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="05868-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="05868-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05868-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="05868-110">Prerequisites</span></span>

<span data-ttu-id="05868-111">To configure Azure AD integration with HR2day by Merces, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="05868-111">To configure Azure AD integration with HR2day by Merces, you need the following items:</span></span>

- <span data-ttu-id="05868-112">An Azure AD subscription.</span><span class="sxs-lookup"><span data-stu-id="05868-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="05868-113">An HR2day by Merces single sign-on enabled subscription.</span><span class="sxs-lookup"><span data-stu-id="05868-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="05868-114">We don't recommend using a production environment to test the steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="05868-114">We don't recommend using a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="05868-115">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="05868-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="05868-116">Don't use your production environment unless it's necessary.</span><span class="sxs-lookup"><span data-stu-id="05868-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="05868-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span><span class="sxs-lookup"><span data-stu-id="05868-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="05868-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="05868-118">Scenario description</span></span>
<span data-ttu-id="05868-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="05868-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="05868-120">The scenario that's outlined here consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="05868-120">The scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="05868-121">Adding HR2day by Merces from the gallery.</span><span class="sxs-lookup"><span data-stu-id="05868-121">Adding HR2day by Merces from the gallery.</span></span>
1. <span data-ttu-id="05868-122">Configuring and testing Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="05868-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-the-gallery"></a><span data-ttu-id="05868-123">Add HR2day by Merces from the gallery</span><span class="sxs-lookup"><span data-stu-id="05868-123">Add HR2day by Merces from the gallery</span></span>
<span data-ttu-id="05868-124">To configure the integration of HR2day by Merces into Azure AD, add HR2day by Merces from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="05868-124">To configure the integration of HR2day by Merces into Azure AD, add HR2day by Merces from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="05868-125">**To add HR2day by Merces from the gallery, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05868-125">**To add HR2day by Merces from the gallery, take the following steps:**</span></span>

1. <span data-ttu-id="05868-126">In the [Azure portal](https://portal.azure.com), on the left navigation pane, select the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="05868-126">In the [Azure portal](https://portal.azure.com), on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="05868-128">Go to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="05868-128">Go to **Enterprise applications**.</span></span> <span data-ttu-id="05868-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="05868-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="05868-131">To add a new application, select the **New application** button on the top of the dialog box.</span><span class="sxs-lookup"><span data-stu-id="05868-131">To add a new application, select the **New application** button on the top of the dialog box.</span></span>

    ![Applications][3]

1. <span data-ttu-id="05868-133">In the search box, type **HR2day by Merces**.</span><span class="sxs-lookup"><span data-stu-id="05868-133">In the search box, type **HR2day by Merces**.</span></span>

    ![Creating an Azure AD test user](./media/hr2day-tutorial/tutorial_hr2daybymerces_search.png)

1. <span data-ttu-id="05868-135">In the results panel, select **HR2day by Merces**, and then select the **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="05868-135">In the results panel, select **HR2day by Merces**, and then select the **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="05868-137">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="05868-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="05868-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="05868-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="05868-139">For single sign-on to work, Azure AD needs to know who the counterpart user in HR2day by Merces is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05868-139">For single sign-on to work, Azure AD needs to know who the counterpart user in HR2day by Merces is to a user in Azure AD.</span></span> <span data-ttu-id="05868-140">In other words, you need to establish a link between an Azure AD user and the related user in HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="05868-140">In other words, you need to establish a link between an Azure AD user and the related user in HR2day by Merces.</span></span>

<span data-ttu-id="05868-141">In HR2day by Merces, assign the **user name** in Azure AD to  **Username** to establish the relationship.</span><span class="sxs-lookup"><span data-stu-id="05868-141">In HR2day by Merces, assign the **user name** in Azure AD to  **Username** to establish the relationship.</span></span>

<span data-ttu-id="05868-142">To configure and test Azure AD single sign-on with HR2day by Merces, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="05868-142">To configure and test Azure AD single sign-on with HR2day by Merces, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="05868-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="05868-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users to use this feature.</span></span>
1. <span data-ttu-id="05868-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05868-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="05868-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="05868-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="05868-146">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="05868-146">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="05868-147">[Test single sign-on](#testing-single-sign-on): Verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="05868-147">[Test single sign-on](#testing-single-sign-on): Verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="05868-148">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="05868-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="05868-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HR2day by Merces application.</span><span class="sxs-lookup"><span data-stu-id="05868-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="05868-150">**To configure Azure AD single sign-on with HR2day by Merces, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05868-150">**To configure Azure AD single sign-on with HR2day by Merces, take the following steps:**</span></span>

1. <span data-ttu-id="05868-151">In the Azure portal, on the **HR2day by Merces** application integration page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="05868-151">In the Azure portal, on the **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![Configure single sign-On][4]

1. <span data-ttu-id="05868-153">To enable single sign-on, in the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="05868-153">To enable single sign-on, in the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Configure single sign-on](./media/hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

1. <span data-ttu-id="05868-155">In the **HR2day by Merces Domain and URLs** section, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="05868-155">In the **HR2day by Merces Domain and URLs** section, take the following steps:</span></span>

    ![Configure single sign-on](./media/hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="05868-157">a.</span><span class="sxs-lookup"><span data-stu-id="05868-157">a.</span></span> <span data-ttu-id="05868-158">In the **Sign-on URL** box, type a URL by using the following pattern: `https://<tenantname>.force.com/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="05868-158">In the **Sign-on URL** box, type a URL by using the following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="05868-159">b.</span><span class="sxs-lookup"><span data-stu-id="05868-159">b.</span></span> <span data-ttu-id="05868-160">In the **Identifier** box, type a URL by using the following pattern: `https://hr2day.force.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="05868-160">In the **Identifier** box, type a URL by using the following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="05868-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="05868-161">These values are not real.</span></span> <span data-ttu-id="05868-162">Update these values with the actual sign-on URL and identifier.</span><span class="sxs-lookup"><span data-stu-id="05868-162">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="05868-163">Contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl) to get these values.</span><span class="sxs-lookup"><span data-stu-id="05868-163">Contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl) to get these values.</span></span> 
 


1. <span data-ttu-id="05868-164">On the **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="05868-164">On the **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save the certificate file on your computer.</span></span>

    ![Configure single sign-on](./media/hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

1. <span data-ttu-id="05868-166">This section describes how to enable users to authenticate to HR2day by Merces with their account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05868-166">This section describes how to enable users to authenticate to HR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="05868-167">They do this by using federation that's based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="05868-167">They do this by using federation that's based on the SAML protocol.</span></span>

    <span data-ttu-id="05868-168">Your HR2day by Merces application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token.</span><span class="sxs-lookup"><span data-stu-id="05868-168">Your HR2day by Merces application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token.</span></span> <span data-ttu-id="05868-169">The following screenshot shows an example of this.</span><span class="sxs-lookup"><span data-stu-id="05868-169">The following screenshot shows an example of this.</span></span> 

    ![Configure single sign-on](./media/hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="05868-171">Before you can configure the SAML assertion, you must contact the [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request the value of the unique identifier attribute for your tenant.</span><span class="sxs-lookup"><span data-stu-id="05868-171">Before you can configure the SAML assertion, you must contact the [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="05868-172">You need this value to complete the steps in the next section.</span><span class="sxs-lookup"><span data-stu-id="05868-172">You need this value to complete the steps in the next section.</span></span> 

1. <span data-ttu-id="05868-173">In the **Single sign-on** dialog box, in the **User Attributes** section, configure the SAML token attribute as shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="05868-173">In the **Single sign-on** dialog box, in the **User Attributes** section, configure the SAML token attribute as shown in the following image.</span></span> <span data-ttu-id="05868-174">Then take the following steps.</span><span class="sxs-lookup"><span data-stu-id="05868-174">Then take the following steps.</span></span>
    
      | <span data-ttu-id="05868-175">Attribute name</span><span class="sxs-lookup"><span data-stu-id="05868-175">Attribute name</span></span>    |   <span data-ttu-id="05868-176">Attribute value</span><span class="sxs-lookup"><span data-stu-id="05868-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="05868-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="05868-177">ATTR_LOGINCLAIM</span></span> | `join([mail],"102938475Z","@"` |
    
      <span data-ttu-id="05868-178">a.</span><span class="sxs-lookup"><span data-stu-id="05868-178">a.</span></span> <span data-ttu-id="05868-179">To open the **Add Attribute** dialog, select **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="05868-179">To open the **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![Configure single sign-on](./media/hr2day-tutorial/tutorial_attribute_04.png)

    ![Configure single sign-On](./media/hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="05868-182">b.</span><span class="sxs-lookup"><span data-stu-id="05868-182">b.</span></span> <span data-ttu-id="05868-183">In the **Name** box, type **ATTR_LOGINCLAIM**.</span><span class="sxs-lookup"><span data-stu-id="05868-183">In the **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="05868-184">c.</span><span class="sxs-lookup"><span data-stu-id="05868-184">c.</span></span> <span data-ttu-id="05868-185">From the **Value** list, select **Join()**.</span><span class="sxs-lookup"><span data-stu-id="05868-185">From the **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="05868-186">d.</span><span class="sxs-lookup"><span data-stu-id="05868-186">d.</span></span> <span data-ttu-id="05868-187">From the **String1** list, select **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="05868-187">From the **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="05868-188">e.</span><span class="sxs-lookup"><span data-stu-id="05868-188">e.</span></span> <span data-ttu-id="05868-189">For **String2**, type the unique identifier that's provided by your HR2day team.</span><span class="sxs-lookup"><span data-stu-id="05868-189">For **String2**, type the unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="05868-190">f.</span><span class="sxs-lookup"><span data-stu-id="05868-190">f.</span></span> <span data-ttu-id="05868-191">In the **Separator** box, type **\@**.</span><span class="sxs-lookup"><span data-stu-id="05868-191">In the **Separator** box, type **\@**.</span></span>
    
    <span data-ttu-id="05868-192">g.</span><span class="sxs-lookup"><span data-stu-id="05868-192">g.</span></span> <span data-ttu-id="05868-193">Select **Ok**.</span><span class="sxs-lookup"><span data-stu-id="05868-193">Select **Ok**.</span></span>

1. <span data-ttu-id="05868-194">Select the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="05868-194">Select the **Save** button.</span></span>

    ![Configure single sign-on](./media/hr2day-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="05868-196">In the **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** to open the **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="05868-196">In the **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="05868-197">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference** section.</span><span class="sxs-lookup"><span data-stu-id="05868-197">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Configure single sign-on](./media/hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

1. <span data-ttu-id="05868-199">To configure SSO  for your application, contact the [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="05868-199">To configure SSO  for your application, contact the [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="05868-200">Attach the downloaded **Certificate(Base64)** file to your email.</span><span class="sxs-lookup"><span data-stu-id="05868-200">Attach the downloaded **Certificate(Base64)** file to your email.</span></span> <span data-ttu-id="05868-201">Also provide the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span><span class="sxs-lookup"><span data-stu-id="05868-201">Also provide the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="05868-202">Mention to the Merces team that this integration needs the Entity ID to be set with the pattern **https://hr2day.force.com/INSTANCENAME**.</span><span class="sxs-lookup"><span data-stu-id="05868-202">Mention to the Merces team that this integration needs the Entity ID to be set with the pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="05868-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="05868-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="05868-204">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab. Then access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="05868-204">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab. Then access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="05868-205">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="05868-205">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="05868-206">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="05868-206">Create an Azure AD test user</span></span>
<span data-ttu-id="05868-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05868-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="05868-209">**To create a test user in Azure AD, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05868-209">**To create a test user in Azure AD, take the following steps:**</span></span>

1. <span data-ttu-id="05868-210">In the **Azure portal**, on the left navigation pane, select the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="05868-210">In the **Azure portal**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/hr2day-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="05868-212">To display the list of users, go to **Users and groups**, and then select **All users**.</span><span class="sxs-lookup"><span data-stu-id="05868-212">To display the list of users, go to **Users and groups**, and then select **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/hr2day-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="05868-214">To open the **User** dialog box, select **Add** on the top of the dialog box.</span><span class="sxs-lookup"><span data-stu-id="05868-214">To open the **User** dialog box, select **Add** on the top of the dialog box.</span></span>
 
    ![Creating an Azure AD test user](./media/hr2day-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="05868-216">In the **User** dialog box, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="05868-216">In the **User** dialog box, take the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="05868-218">a.</span><span class="sxs-lookup"><span data-stu-id="05868-218">a.</span></span> <span data-ttu-id="05868-219">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05868-219">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="05868-220">b.</span><span class="sxs-lookup"><span data-stu-id="05868-220">b.</span></span> <span data-ttu-id="05868-221">In the **User name** box, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="05868-221">In the **User name** box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="05868-222">c.</span><span class="sxs-lookup"><span data-stu-id="05868-222">c.</span></span> <span data-ttu-id="05868-223">Select **Show Password**, and then write down the password.</span><span class="sxs-lookup"><span data-stu-id="05868-223">Select **Show Password**, and then write down the password.</span></span>

    <span data-ttu-id="05868-224">d.</span><span class="sxs-lookup"><span data-stu-id="05868-224">d.</span></span> <span data-ttu-id="05868-225">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="05868-225">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="05868-226">Create an HR2day by Merces test user</span><span class="sxs-lookup"><span data-stu-id="05868-226">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="05868-227">The objective of this section is to create a user called Britta Simon in HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="05868-227">The objective of this section is to create a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="05868-228">To add the users in the HR2day account, work with the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="05868-228">To add the users in the HR2day account, work with the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="05868-229">If you need to create a user manually, contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="05868-229">If you need to create a user manually, contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="05868-230">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="05868-230">Assign the Azure AD test user</span></span>

<span data-ttu-id="05868-231">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="05868-231">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to HR2day by Merces.</span></span>

![Assign user][200] 

<span data-ttu-id="05868-233">**To assign Britta Simon to HR2day by Merces, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="05868-233">**To assign Britta Simon to HR2day by Merces, take the following steps:**</span></span>

1. <span data-ttu-id="05868-234">In the Azure portal, open the applications view, go to the directory view, and then go to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="05868-234">In the Azure portal, open the applications view, go to the directory view, and then go to **Enterprise applications**.</span></span> <span data-ttu-id="05868-235">Next, select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="05868-235">Next, select **All applications**.</span></span>

    ![Assign user][201] 

1. <span data-ttu-id="05868-237">In the applications list, select **HR2day by Merces**.</span><span class="sxs-lookup"><span data-stu-id="05868-237">In the applications list, select **HR2day by Merces**.</span></span>

    ![Configure single sign-on](./media/hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

1. <span data-ttu-id="05868-239">In the menu on the left, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="05868-239">In the menu on the left, select **Users and groups**.</span></span>

    ![Assign user][202] 

1. <span data-ttu-id="05868-241">Select the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="05868-241">Select the **Add** button.</span></span> <span data-ttu-id="05868-242">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="05868-242">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Assign user][203]

1. <span data-ttu-id="05868-244">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="05868-244">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

1. <span data-ttu-id="05868-245">Click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="05868-245">Click the **Select** button.</span></span>

1. <span data-ttu-id="05868-246">In the **Add Assignment** dialog box, select **Assign**.</span><span class="sxs-lookup"><span data-stu-id="05868-246">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="05868-247">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="05868-247">Test single sign-on</span></span>

<span data-ttu-id="05868-248">The objective of this section is to test your Azure AD single sign-on configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="05868-248">The objective of this section is to test your Azure AD single sign-on configuration by using the Access Panel.</span></span>  

<span data-ttu-id="05868-249">When you select the HR2day by Merces tile in the Access Panel, you automatically get signed in  to your HR2day by Merces application.</span><span class="sxs-lookup"><span data-stu-id="05868-249">When you select the HR2day by Merces tile in the Access Panel, you automatically get signed in  to your HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="05868-250">Additional resources</span><span class="sxs-lookup"><span data-stu-id="05868-250">Additional resources</span></span>

* [<span data-ttu-id="05868-251">List of tutorials about how to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05868-251">List of tutorials about how to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="05868-252">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="05868-252">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/hr2day-tutorial/tutorial_general_01.png
[2]: ./media/hr2day-tutorial/tutorial_general_02.png
[3]: ./media/hr2day-tutorial/tutorial_general_03.png
[4]: ./media/hr2day-tutorial/tutorial_general_04.png

[100]: ./media/hr2day-tutorial/tutorial_general_100.png

[200]: ./media/hr2day-tutorial/tutorial_general_200.png
[201]: ./media/hr2day-tutorial/tutorial_general_201.png
[202]: ./media/hr2day-tutorial/tutorial_general_202.png
[203]: ./media/hr2day-tutorial/tutorial_general_203.png

