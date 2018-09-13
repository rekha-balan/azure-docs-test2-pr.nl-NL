---
title: 'Tutorial: Azure Active Directory integration with iQualify LMS | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and iQualify LMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 8a3caaff-dd8d-4afd-badf-a0fd60db3d2c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/04/2017
ms.author: jeedes
ms.openlocfilehash: d1161480bfd7a4cfeeb81f02234586a515fdffed
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967799"
---
# <a name="tutorial-azure-active-directory-integration-with-iqualify-lms"></a><span data-ttu-id="679e2-103">Tutorial: Azure Active Directory integration with iQualify LMS</span><span class="sxs-lookup"><span data-stu-id="679e2-103">Tutorial: Azure Active Directory integration with iQualify LMS</span></span>

<span data-ttu-id="679e2-104">In this tutorial, you learn how to integrate iQualify LMS with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="679e2-104">In this tutorial, you learn how to integrate iQualify LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="679e2-105">Integrating iQualify LMS with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="679e2-105">Integrating iQualify LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="679e2-106">You can control in Azure AD who has access to iQualify LMS.</span><span class="sxs-lookup"><span data-stu-id="679e2-106">You can control in Azure AD who has access to iQualify LMS.</span></span>
- <span data-ttu-id="679e2-107">You can enable your users to automatically get signed-on to iQualify LMS (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="679e2-107">You can enable your users to automatically get signed-on to iQualify LMS (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="679e2-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="679e2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="679e2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="679e2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="679e2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="679e2-110">Prerequisites</span></span>

<span data-ttu-id="679e2-111">To configure Azure AD integration with iQualify LMS, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="679e2-111">To configure Azure AD integration with iQualify LMS, you need the following items:</span></span>

- <span data-ttu-id="679e2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="679e2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="679e2-113">An iQualify LMS single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="679e2-113">An iQualify LMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="679e2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="679e2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="679e2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="679e2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="679e2-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="679e2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="679e2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="679e2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="679e2-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="679e2-118">Scenario description</span></span>
<span data-ttu-id="679e2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="679e2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="679e2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="679e2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="679e2-121">Adding iQualify LMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="679e2-121">Adding iQualify LMS from the gallery</span></span>
1. <span data-ttu-id="679e2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="679e2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iqualify-lms-from-the-gallery"></a><span data-ttu-id="679e2-123">Adding iQualify LMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="679e2-123">Adding iQualify LMS from the gallery</span></span>
<span data-ttu-id="679e2-124">To configure the integration of iQualify LMS into Azure AD, you need to add iQualify LMS from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="679e2-124">To configure the integration of iQualify LMS into Azure AD, you need to add iQualify LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="679e2-125">**To add iQualify LMS from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="679e2-125">**To add iQualify LMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="679e2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="679e2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="679e2-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="679e2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="679e2-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="679e2-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="679e2-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="679e2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="679e2-133">In the search box, type **iQualify LMS**, select **iQualify LMS** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="679e2-133">In the search box, type **iQualify LMS**, select **iQualify LMS** from result panel then click **Add** button to add the application.</span></span>

    ![iQualify LMS in the results list](./media/iqualify-tutorial/tutorial_iqualify_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="679e2-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="679e2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="679e2-136">In this section, you configure and test Azure AD single sign-on with iQualify LMS based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="679e2-136">In this section, you configure and test Azure AD single sign-on with iQualify LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="679e2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in iQualify LMS is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="679e2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in iQualify LMS is to a user in Azure AD.</span></span> <span data-ttu-id="679e2-138">In other words, a link relationship between an Azure AD user and the related user in iQualify LMS needs to be established.</span><span class="sxs-lookup"><span data-stu-id="679e2-138">In other words, a link relationship between an Azure AD user and the related user in iQualify LMS needs to be established.</span></span>

<span data-ttu-id="679e2-139">In iQualify LMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="679e2-139">In iQualify LMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="679e2-140">To configure and test Azure AD single sign-on with iQualify LMS, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="679e2-140">To configure and test Azure AD single sign-on with iQualify LMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="679e2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="679e2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="679e2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="679e2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="679e2-143">**[Create an iQualify LMS test user](#create-an-iqualify-lms-test-user)** - to have a counterpart of Britta Simon in iQualify LMS that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="679e2-143">**[Create an iQualify LMS test user](#create-an-iqualify-lms-test-user)** - to have a counterpart of Britta Simon in iQualify LMS that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="679e2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="679e2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="679e2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="679e2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="679e2-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="679e2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="679e2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iQualify LMS application.</span><span class="sxs-lookup"><span data-stu-id="679e2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iQualify LMS application.</span></span>

<span data-ttu-id="679e2-148">**To configure Azure AD single sign-on with iQualify LMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="679e2-148">**To configure Azure AD single sign-on with iQualify LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="679e2-149">In the Azure portal, on the **iQualify LMS** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="679e2-149">In the Azure portal, on the **iQualify LMS** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="679e2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="679e2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/iqualify-tutorial/tutorial_iqualify_samlbase.png)

1. <span data-ttu-id="679e2-153">On the **iQualify LMS Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span><span class="sxs-lookup"><span data-stu-id="679e2-153">On the **iQualify LMS Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![iQualify LMS Domain and URLs single sign-on information](./media/iqualify-tutorial/tutorial_iqualify_url.png)

    <span data-ttu-id="679e2-155">a.</span><span class="sxs-lookup"><span data-stu-id="679e2-155">a.</span></span> <span data-ttu-id="679e2-156">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="679e2-156">In the **Identifier** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|--|
    | <span data-ttu-id="679e2-157">Production Environment: `https://<yourorg>.iqualify.com/`</span><span class="sxs-lookup"><span data-stu-id="679e2-157">Production Environment: `https://<yourorg>.iqualify.com/`</span></span>|
    | <span data-ttu-id="679e2-158">Test Environment: `https://<yourorg>.iqualify.io`</span><span class="sxs-lookup"><span data-stu-id="679e2-158">Test Environment: `https://<yourorg>.iqualify.io`</span></span>|
    
    <span data-ttu-id="679e2-159">b.</span><span class="sxs-lookup"><span data-stu-id="679e2-159">b.</span></span> <span data-ttu-id="679e2-160">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="679e2-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|--|
    | <span data-ttu-id="679e2-161">Production Environment: `https://<yourorg>.iqualify.com/auth/saml2/callback`</span><span class="sxs-lookup"><span data-stu-id="679e2-161">Production Environment: `https://<yourorg>.iqualify.com/auth/saml2/callback`</span></span> |
    | <span data-ttu-id="679e2-162">Test Environment: `https://<yourorg>.iqualify.io/auth/saml2/callback`</span><span class="sxs-lookup"><span data-stu-id="679e2-162">Test Environment: `https://<yourorg>.iqualify.io/auth/saml2/callback`</span></span> |

1. <span data-ttu-id="679e2-163">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="679e2-163">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![iQualify LMS Domain and URLs single sign-on information](./media/iqualify-tutorial/tutorial_iqualify_url1.png)

    <span data-ttu-id="679e2-165">In the **Sign-on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="679e2-165">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|--|
    | <span data-ttu-id="679e2-166">Production Environment: `https://<yourorg>.iqualify.com/login`</span><span class="sxs-lookup"><span data-stu-id="679e2-166">Production Environment: `https://<yourorg>.iqualify.com/login`</span></span> |
    | <span data-ttu-id="679e2-167">Test Environment: `https://<yourorg>.iqualify.io/login`</span><span class="sxs-lookup"><span data-stu-id="679e2-167">Test Environment: `https://<yourorg>.iqualify.io/login`</span></span> |
     
    > [!NOTE] 
    > <span data-ttu-id="679e2-168">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="679e2-168">These values are not real.</span></span> <span data-ttu-id="679e2-169">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="679e2-169">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="679e2-170">Contact [iQualify LMS Client support team](https://www.iqualify.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="679e2-170">Contact [iQualify LMS Client support team](https://www.iqualify.com) to get these values.</span></span> 

1. <span data-ttu-id="679e2-171">The iQualify LMS application expects the Security Assertion Markup Language (SAML) assertions to be displayed in a specific format.</span><span class="sxs-lookup"><span data-stu-id="679e2-171">The iQualify LMS application expects the Security Assertion Markup Language (SAML) assertions to be displayed in a specific format.</span></span> <span data-ttu-id="679e2-172">Configure the claims and manage the values of the attributes in the **User Attributes** section of the iQualify application integration page, as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="679e2-172">Configure the claims and manage the values of the attributes in the **User Attributes** section of the iQualify application integration page, as shown in the following screenshot:</span></span>
    
    ![Configure Single Sign-On](./media/iqualify-tutorial/atb.png)

1. <span data-ttu-id="679e2-174">In the **User Attributes** section on the **Single sign-on** dialog  perform the following steps for each row shown in the table below:</span><span class="sxs-lookup"><span data-stu-id="679e2-174">In the **User Attributes** section on the **Single sign-on** dialog  perform the following steps for each row shown in the table below:</span></span>
    
    | <span data-ttu-id="679e2-175">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="679e2-175">Attribute Name</span></span> | <span data-ttu-id="679e2-176">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="679e2-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="679e2-177">email</span><span class="sxs-lookup"><span data-stu-id="679e2-177">email</span></span> | <span data-ttu-id="679e2-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="679e2-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="679e2-179">first_name</span><span class="sxs-lookup"><span data-stu-id="679e2-179">first_name</span></span> | <span data-ttu-id="679e2-180">user.givenname</span><span class="sxs-lookup"><span data-stu-id="679e2-180">user.givenname</span></span> |
    | <span data-ttu-id="679e2-181">last_name</span><span class="sxs-lookup"><span data-stu-id="679e2-181">last_name</span></span> | <span data-ttu-id="679e2-182">user.surname</span><span class="sxs-lookup"><span data-stu-id="679e2-182">user.surname</span></span> |
    | <span data-ttu-id="679e2-183">person_id</span><span class="sxs-lookup"><span data-stu-id="679e2-183">person_id</span></span> | <span data-ttu-id="679e2-184">"your attribute"</span><span class="sxs-lookup"><span data-stu-id="679e2-184">"your attribute"</span></span> | 

    <span data-ttu-id="679e2-185">a.</span><span class="sxs-lookup"><span data-stu-id="679e2-185">a.</span></span> <span data-ttu-id="679e2-186">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="679e2-186">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/iqualify-tutorial/atb2.png)

    ![Configure Single Sign-On](./media/iqualify-tutorial/atb3.png)
    
    <span data-ttu-id="679e2-189">b.</span><span class="sxs-lookup"><span data-stu-id="679e2-189">b.</span></span> <span data-ttu-id="679e2-190">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="679e2-190">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="679e2-191">c.</span><span class="sxs-lookup"><span data-stu-id="679e2-191">c.</span></span> <span data-ttu-id="679e2-192">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="679e2-192">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="679e2-193">d.</span><span class="sxs-lookup"><span data-stu-id="679e2-193">d.</span></span> <span data-ttu-id="679e2-194">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="679e2-194">Click **Ok**</span></span>

    <span data-ttu-id="679e2-195">e.</span><span class="sxs-lookup"><span data-stu-id="679e2-195">e.</span></span> <span data-ttu-id="679e2-196">Repeat steps "a" through "d" for the next table rows.</span><span class="sxs-lookup"><span data-stu-id="679e2-196">Repeat steps "a" through "d" for the next table rows.</span></span> 

    > [!Note]
    > <span data-ttu-id="679e2-197">Repeating steps "a" through "d" for the **person_id** attribute is **Optional**</span><span class="sxs-lookup"><span data-stu-id="679e2-197">Repeating steps "a" through "d" for the **person_id** attribute is **Optional**</span></span>

1. <span data-ttu-id="679e2-198">On the **SAML Signing Certificate** section, click **Certificate (Base 64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="679e2-198">On the **SAML Signing Certificate** section, click **Certificate (Base 64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/iqualify-tutorial/tutorial_iqualify_certificate.png) 

1. <span data-ttu-id="679e2-200">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="679e2-200">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/iqualify-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="679e2-202">On the **iQualify LMS Configuration** section, click **Configure iQualify LMS** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="679e2-202">On the **iQualify LMS Configuration** section, click **Configure iQualify LMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="679e2-203">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="679e2-203">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![iQualify LMS Configuration](./media/iqualify-tutorial/tutorial_iqualify_configure.png) 

1.  <span data-ttu-id="679e2-205">Open a new browser window, and then sign in to your iQualify environment as an administrator.</span><span class="sxs-lookup"><span data-stu-id="679e2-205">Open a new browser window, and then sign in to your iQualify environment as an administrator.</span></span>

1. <span data-ttu-id="679e2-206">Once you are logged in, click on your avatar at the top right, then click on **"Account settings."**</span><span class="sxs-lookup"><span data-stu-id="679e2-206">Once you are logged in, click on your avatar at the top right, then click on **"Account settings."**</span></span>

    ![Account settings](./media/iqualify-tutorial/setting1.png) 
1. <span data-ttu-id="679e2-208">In the account settings area, click on the ribbon menu on the left and click on **"INTEGRATIONS."**</span><span class="sxs-lookup"><span data-stu-id="679e2-208">In the account settings area, click on the ribbon menu on the left and click on **"INTEGRATIONS."**</span></span>
    
    ![INTEGRATIONS](./media/iqualify-tutorial/setting2.png)

1. <span data-ttu-id="679e2-210">Under INTEGRATIONS, click on the **SAML** icon.</span><span class="sxs-lookup"><span data-stu-id="679e2-210">Under INTEGRATIONS, click on the **SAML** icon.</span></span>

    ![SAML icon](./media/iqualify-tutorial/setting3.png)

1. <span data-ttu-id="679e2-212">In the **SAML Authentication Settings** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="679e2-212">In the **SAML Authentication Settings** dialog box, perform the following steps:</span></span>

    ![SAML Authentication Settings](./media/iqualify-tutorial/setting4.png)

    <span data-ttu-id="679e2-214">a.</span><span class="sxs-lookup"><span data-stu-id="679e2-214">a.</span></span> <span data-ttu-id="679e2-215">In the **SAML SINGLE SIGN-ON SERVICE URL** box, paste the **SAML Single Sign‑On Service URL** value copied from the Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="679e2-215">In the **SAML SINGLE SIGN-ON SERVICE URL** box, paste the **SAML Single Sign‑On Service URL** value copied from the Azure AD application configuration window.</span></span>
    
    <span data-ttu-id="679e2-216">b.</span><span class="sxs-lookup"><span data-stu-id="679e2-216">b.</span></span> <span data-ttu-id="679e2-217">In the **SAML LOGOUT URL** box, paste the **Sign‑Out URL** value copied from the Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="679e2-217">In the **SAML LOGOUT URL** box, paste the **Sign‑Out URL** value copied from the Azure AD application configuration window.</span></span>
    
    <span data-ttu-id="679e2-218">c.</span><span class="sxs-lookup"><span data-stu-id="679e2-218">c.</span></span> <span data-ttu-id="679e2-219">Open the downloaded certificate file in notepad, copy the content, and then paste it in the **PUBLIC CERTIFICATE** box.</span><span class="sxs-lookup"><span data-stu-id="679e2-219">Open the downloaded certificate file in notepad, copy the content, and then paste it in the **PUBLIC CERTIFICATE** box.</span></span>
    
    <span data-ttu-id="679e2-220">d.</span><span class="sxs-lookup"><span data-stu-id="679e2-220">d.</span></span> <span data-ttu-id="679e2-221">In **LOGIN BUTTON LABEL** enter the name for the button to be displayed on login page.</span><span class="sxs-lookup"><span data-stu-id="679e2-221">In **LOGIN BUTTON LABEL** enter the name for the button to be displayed on login page.</span></span>
    
    <span data-ttu-id="679e2-222">e.</span><span class="sxs-lookup"><span data-stu-id="679e2-222">e.</span></span> <span data-ttu-id="679e2-223">Click **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="679e2-223">Click **SAVE**.</span></span>

    <span data-ttu-id="679e2-224">f.</span><span class="sxs-lookup"><span data-stu-id="679e2-224">f.</span></span> <span data-ttu-id="679e2-225">Click **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="679e2-225">Click **UPDATE**.</span></span>

> [!TIP]
> <span data-ttu-id="679e2-226">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="679e2-226">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="679e2-227">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="679e2-227">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="679e2-228">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="679e2-228">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="679e2-229">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="679e2-229">Create an Azure AD test user</span></span>

<span data-ttu-id="679e2-230">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="679e2-230">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="679e2-232">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="679e2-232">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="679e2-233">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="679e2-233">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/iqualify-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="679e2-235">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="679e2-235">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/iqualify-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="679e2-237">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="679e2-237">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/iqualify-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="679e2-239">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="679e2-239">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/iqualify-tutorial/create_aaduser_04.png)

    <span data-ttu-id="679e2-241">a.</span><span class="sxs-lookup"><span data-stu-id="679e2-241">a.</span></span> <span data-ttu-id="679e2-242">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="679e2-242">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="679e2-243">b.</span><span class="sxs-lookup"><span data-stu-id="679e2-243">b.</span></span> <span data-ttu-id="679e2-244">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="679e2-244">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="679e2-245">c.</span><span class="sxs-lookup"><span data-stu-id="679e2-245">c.</span></span> <span data-ttu-id="679e2-246">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="679e2-246">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="679e2-247">d.</span><span class="sxs-lookup"><span data-stu-id="679e2-247">d.</span></span> <span data-ttu-id="679e2-248">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="679e2-248">Click **Create**.</span></span>
 
### <a name="create-an-iqualify-lms-test-user"></a><span data-ttu-id="679e2-249">Create an iQualify LMS test user</span><span class="sxs-lookup"><span data-stu-id="679e2-249">Create an iQualify LMS test user</span></span>

<span data-ttu-id="679e2-250">In this section, a user called Britta Simon is created in iQualify.</span><span class="sxs-lookup"><span data-stu-id="679e2-250">In this section, a user called Britta Simon is created in iQualify.</span></span> <span data-ttu-id="679e2-251">iQualify LMS supports just‑in‑time user provisioning, which is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="679e2-251">iQualify LMS supports just‑in‑time user provisioning, which is enabled by default.</span></span>

<span data-ttu-id="679e2-252">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="679e2-252">There is no action item for you in this section.</span></span> <span data-ttu-id="679e2-253">If a user doesn't already exist in iQualify, a new one is created when you attempt to access iQualify LMS.</span><span class="sxs-lookup"><span data-stu-id="679e2-253">If a user doesn't already exist in iQualify, a new one is created when you attempt to access iQualify LMS.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="679e2-254">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="679e2-254">Assign the Azure AD test user</span></span>

<span data-ttu-id="679e2-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to iQualify LMS.</span><span class="sxs-lookup"><span data-stu-id="679e2-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to iQualify LMS.</span></span>

![Assign the user role][200] 

<span data-ttu-id="679e2-257">**To assign Britta Simon to iQualify LMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="679e2-257">**To assign Britta Simon to iQualify LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="679e2-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="679e2-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="679e2-260">In the applications list, select **iQualify LMS**.</span><span class="sxs-lookup"><span data-stu-id="679e2-260">In the applications list, select **iQualify LMS**.</span></span>

    ![The iQualify LMS link in the Applications list](./media/iqualify-tutorial/tutorial_iqualify_app.png)  

1. <span data-ttu-id="679e2-262">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="679e2-262">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="679e2-264">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="679e2-264">Click **Add** button.</span></span> <span data-ttu-id="679e2-265">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="679e2-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="679e2-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="679e2-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="679e2-268">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="679e2-268">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="679e2-269">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="679e2-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="679e2-270">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="679e2-270">Test single sign-on</span></span>

<span data-ttu-id="679e2-271">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="679e2-271">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="679e2-272">When you click the iQualify LMS tile in the Access Panel, you should get login page of your iQualify LMS application.</span><span class="sxs-lookup"><span data-stu-id="679e2-272">When you click the iQualify LMS tile in the Access Panel, you should get login page of your iQualify LMS application.</span></span> 

   ![login page](./media/iqualify-tutorial/login.png) 

<span data-ttu-id="679e2-274">Click **Sign in with Azure AD** button and you should get automatically signed-on to your iQualify LMS application.</span><span class="sxs-lookup"><span data-stu-id="679e2-274">Click **Sign in with Azure AD** button and you should get automatically signed-on to your iQualify LMS application.</span></span>

<span data-ttu-id="679e2-275">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="679e2-275">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="679e2-276">Additional resources</span><span class="sxs-lookup"><span data-stu-id="679e2-276">Additional resources</span></span>

* [<span data-ttu-id="679e2-277">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="679e2-277">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="679e2-278">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="679e2-278">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/iqualify-tutorial/tutorial_general_01.png
[2]: ./media/iqualify-tutorial/tutorial_general_02.png
[3]: ./media/iqualify-tutorial/tutorial_general_03.png
[4]: ./media/iqualify-tutorial/tutorial_general_04.png

[100]: ./media/iqualify-tutorial/tutorial_general_100.png

[200]: ./media/iqualify-tutorial/tutorial_general_200.png
[201]: ./media/iqualify-tutorial/tutorial_general_201.png
[202]: ./media/iqualify-tutorial/tutorial_general_202.png
[203]: ./media/iqualify-tutorial/tutorial_general_203.png

