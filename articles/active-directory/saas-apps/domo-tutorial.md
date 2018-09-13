---
title: 'Tutorial: Azure Active Directory integration with Domo | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Domo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 058626e4-73b3-4dc2-86ca-b060d002d70a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: jeedes
ms.openlocfilehash: 9c6a8585033cc9ba8db763e053f63cef47fdcd02
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865146"
---
# <a name="tutorial-azure-active-directory-integration-with-domo"></a><span data-ttu-id="9b9d3-103">Tutorial: Azure Active Directory integration with Domo</span><span class="sxs-lookup"><span data-stu-id="9b9d3-103">Tutorial: Azure Active Directory integration with Domo</span></span>

<span data-ttu-id="9b9d3-104">In this tutorial, you learn how to integrate Domo with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9b9d3-104">In this tutorial, you learn how to integrate Domo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9b9d3-105">Integrating Domo with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9b9d3-105">Integrating Domo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9b9d3-106">You can control in Azure AD who has access to Domo</span><span class="sxs-lookup"><span data-stu-id="9b9d3-106">You can control in Azure AD who has access to Domo</span></span>
- <span data-ttu-id="9b9d3-107">You can enable your users to automatically get signed-on to Domo (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="9b9d3-107">You can enable your users to automatically get signed-on to Domo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9b9d3-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9b9d3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9b9d3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="9b9d3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b9d3-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9b9d3-110">Prerequisites</span></span>

<span data-ttu-id="9b9d3-111">To configure Azure AD integration with Domo, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9b9d3-111">To configure Azure AD integration with Domo, you need the following items:</span></span>

- <span data-ttu-id="9b9d3-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9b9d3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9b9d3-113">A Domo single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9b9d3-113">A Domo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9b9d3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9b9d3-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9b9d3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9b9d3-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9b9d3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9b9d3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9b9d3-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="9b9d3-118">Scenario description</span></span>
<span data-ttu-id="9b9d3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9b9d3-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9b9d3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9b9d3-121">Adding Domo from the gallery</span><span class="sxs-lookup"><span data-stu-id="9b9d3-121">Adding Domo from the gallery</span></span>
1. <span data-ttu-id="9b9d3-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9b9d3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-domo-from-the-gallery"></a><span data-ttu-id="9b9d3-123">Adding Domo from the gallery</span><span class="sxs-lookup"><span data-stu-id="9b9d3-123">Adding Domo from the gallery</span></span>
<span data-ttu-id="9b9d3-124">To configure the integration of Domo into Azure AD, you need to add Domo from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-124">To configure the integration of Domo into Azure AD, you need to add Domo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9b9d3-125">**To add Domo from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9b9d3-125">**To add Domo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9b9d3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="9b9d3-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9b9d3-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="9b9d3-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="9b9d3-133">In the search box, type **Domo**.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-133">In the search box, type **Domo**.</span></span>

    ![Creating an Azure AD test user](./media/domo-tutorial/tutorial_domo_search.png)

1. <span data-ttu-id="9b9d3-135">In the results panel, select **Domo**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-135">In the results panel, select **Domo**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/domo-tutorial/tutorial_domo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9b9d3-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9b9d3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9b9d3-138">In this section, you configure and test Azure AD single sign-on with Domo based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="9b9d3-138">In this section, you configure and test Azure AD single sign-on with Domo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9b9d3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Domo is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Domo is to a user in Azure AD.</span></span> <span data-ttu-id="9b9d3-140">In other words, a link relationship between an Azure AD user and the related user in Domo needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-140">In other words, a link relationship between an Azure AD user and the related user in Domo needs to be established.</span></span>

<span data-ttu-id="9b9d3-141">In Domo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-141">In Domo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9b9d3-142">To configure and test Azure AD single sign-on with Domo, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9b9d3-142">To configure and test Azure AD single sign-on with Domo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9b9d3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="9b9d3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="9b9d3-145">**[Creating a Domo test user](#creating-a-domo-test-user)** - to have a counterpart of Britta Simon in Domo that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-145">**[Creating a Domo test user](#creating-a-domo-test-user)** - to have a counterpart of Britta Simon in Domo that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="9b9d3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="9b9d3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9b9d3-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9b9d3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9b9d3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Domo application.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Domo application.</span></span>

<span data-ttu-id="9b9d3-150">**To configure Azure AD single sign-on with Domo, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9b9d3-150">**To configure Azure AD single sign-on with Domo, perform the following steps:**</span></span>

1. <span data-ttu-id="9b9d3-151">In the Azure portal, on the **Domo** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-151">In the Azure portal, on the **Domo** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="9b9d3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/domo-tutorial/tutorial_domo_samlbase.png)

1. <span data-ttu-id="9b9d3-155">On the **Domo Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9b9d3-155">On the **Domo Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/domo-tutorial/tutorial_domo_url.png)

    <span data-ttu-id="9b9d3-157">a.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-157">a.</span></span> <span data-ttu-id="9b9d3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.domo.com`</span><span class="sxs-lookup"><span data-stu-id="9b9d3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.domo.com`</span></span>

    <span data-ttu-id="9b9d3-159">b.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-159">b.</span></span> <span data-ttu-id="9b9d3-160">In the **Identifier** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="9b9d3-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span>     

    | |
    |--|    
    | `https://<companyname>.domo.com` |
    | `https://<companyname>.beta.domo.com` |
    | `https://<companyname>.demo.domo.com` |
    | `https://<companyname>.dev.domo.com` | 
    | `https://<companyname>.fastage1.domo.com` |       
    | `https://<companyname>.frdev.domo.com` |       
    | `https://<companyname>.gastage.domo.com` |       
    | `https://<companyname>.load.domo.com` |       
    | `https://<companyname>.local.domo.com` |       
    | `https://<companyname>.qa.domo.com` |
    | `https://<companyname>.stage.domo.com` |
    
    > [!NOTE] 
    > <span data-ttu-id="9b9d3-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-161">These values are not real.</span></span> <span data-ttu-id="9b9d3-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9b9d3-163">Contact [Domo Client support team](mailto:support@domo.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-163">Contact [Domo Client support team](mailto:support@domo.com) to get these values.</span></span>

1. <span data-ttu-id="9b9d3-164">Domo application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-164">Domo application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="9b9d3-165">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-165">Configure the following claims for this application.</span></span> <span data-ttu-id="9b9d3-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="9b9d3-167">The following screenshot shows an example for this configuration.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-167">The following screenshot shows an example for this configuration.</span></span> 

    ![Configure Single Sign-On](./media/domo-tutorial/tutorial_domo_attributes.png)
    
1. <span data-ttu-id="9b9d3-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9b9d3-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="9b9d3-170">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="9b9d3-170">Attribute Name</span></span> | <span data-ttu-id="9b9d3-171">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="9b9d3-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="9b9d3-172">name</span><span class="sxs-lookup"><span data-stu-id="9b9d3-172">name</span></span> | <span data-ttu-id="9b9d3-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="9b9d3-173">user.displayname</span></span> |
    | <span data-ttu-id="9b9d3-174">email</span><span class="sxs-lookup"><span data-stu-id="9b9d3-174">email</span></span> | <span data-ttu-id="9b9d3-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="9b9d3-175">user.mail</span></span> |
    
    <span data-ttu-id="9b9d3-176">a.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-176">a.</span></span> <span data-ttu-id="9b9d3-177">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/domo-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/domo-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="9b9d3-180">b.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-180">b.</span></span> <span data-ttu-id="9b9d3-181">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="9b9d3-182">c.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-182">c.</span></span> <span data-ttu-id="9b9d3-183">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="9b9d3-184">d.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-184">d.</span></span> <span data-ttu-id="9b9d3-185">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-185">Click **Ok**.</span></span> 
 
1. <span data-ttu-id="9b9d3-186">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-186">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/domo-tutorial/tutorial_domo_certificate.png) 

1. <span data-ttu-id="9b9d3-188">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-188">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/domo-tutorial/tutorial_general_400.png)


1. <span data-ttu-id="9b9d3-190">On the **Domo Configuration** section, click **Configure Domo** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-190">On the **Domo Configuration** section, click **Configure Domo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9b9d3-191">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="9b9d3-191">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>   

   ![Configure Single Sign-On](./media/domo-tutorial/tutorial_domo_configure.png) 

1. <span data-ttu-id="9b9d3-193">To configure single sign-on on **Domo** side, please navigate to Domo's Knowledge Base article found [here](http://knowledge.domo.com?cid=azuread), and follow the instructions.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-193">To configure single sign-on on **Domo** side, please navigate to Domo's Knowledge Base article found [here](http://knowledge.domo.com?cid=azuread), and follow the instructions.</span></span>

> [!TIP]
> <span data-ttu-id="9b9d3-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="9b9d3-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9b9d3-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9b9d3-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9b9d3-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9b9d3-197">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9b9d3-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="9b9d3-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="9b9d3-200">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9b9d3-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9b9d3-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/domo-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="9b9d3-203">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/domo-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="9b9d3-205">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/domo-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="9b9d3-207">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9b9d3-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/domo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9b9d3-209">a.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-209">a.</span></span> <span data-ttu-id="9b9d3-210">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9b9d3-211">b.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-211">b.</span></span> <span data-ttu-id="9b9d3-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9b9d3-213">c.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-213">c.</span></span> <span data-ttu-id="9b9d3-214">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9b9d3-215">d.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-215">d.</span></span> <span data-ttu-id="9b9d3-216">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-216">Click **Create**.</span></span>
 
### <a name="creating-a-domo-test-user"></a><span data-ttu-id="9b9d3-217">Creating a Domo test user</span><span class="sxs-lookup"><span data-stu-id="9b9d3-217">Creating a Domo test user</span></span>

<span data-ttu-id="9b9d3-218">The objective of this section is to create a user called Britta Simon in Domo.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-218">The objective of this section is to create a user called Britta Simon in Domo.</span></span> <span data-ttu-id="9b9d3-219">Domo supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-219">Domo supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="9b9d3-220">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-220">There is no action item for you in this section.</span></span> <span data-ttu-id="9b9d3-221">A new user is created during an attempt to access Domo if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-221">A new user is created during an attempt to access Domo if it doesn't exist yet.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9b9d3-222">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9b9d3-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9b9d3-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Domo.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Domo.</span></span>

![Assign User][200] 

<span data-ttu-id="9b9d3-225">**To assign Britta Simon to Domo, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9b9d3-225">**To assign Britta Simon to Domo, perform the following steps:**</span></span>

1. <span data-ttu-id="9b9d3-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="9b9d3-228">In the applications list, select **Domo**.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-228">In the applications list, select **Domo**.</span></span>

    ![Configure Single Sign-On](./media/domo-tutorial/tutorial_domo_app.png) 

1. <span data-ttu-id="9b9d3-230">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="9b9d3-232">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-232">Click **Add** button.</span></span> <span data-ttu-id="9b9d3-233">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="9b9d3-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="9b9d3-236">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-236">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="9b9d3-237">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9b9d3-238">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="9b9d3-238">Testing single sign-on</span></span>

<span data-ttu-id="9b9d3-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="9b9d3-240">When you click the Domo tile in the Access Panel, you should get automatically signed-on to your Domo application.</span><span class="sxs-lookup"><span data-stu-id="9b9d3-240">When you click the Domo tile in the Access Panel, you should get automatically signed-on to your Domo application.</span></span>

<span data-ttu-id="9b9d3-241">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9b9d3-241">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9b9d3-242">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9b9d3-242">Additional resources</span></span>

* [<span data-ttu-id="9b9d3-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b9d3-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="9b9d3-244">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9b9d3-244">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/domo-tutorial/tutorial_general_01.png
[2]: ./media/domo-tutorial/tutorial_general_02.png
[3]: ./media/domo-tutorial/tutorial_general_03.png
[4]: ./media/domo-tutorial/tutorial_general_04.png

[100]: ./media/domo-tutorial/tutorial_general_100.png

[200]: ./media/domo-tutorial/tutorial_general_200.png
[201]: ./media/domo-tutorial/tutorial_general_201.png
[202]: ./media/domo-tutorial/tutorial_general_202.png
[203]: ./media/domo-tutorial/tutorial_general_203.png

