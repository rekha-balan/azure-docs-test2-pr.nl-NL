---
title: 'Tutorial: Azure Active Directory integration with ADP Globalview | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ADP Globalview.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 11a3df06cbd1c3f34bfd5b04c1f6dfc41cab8187
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868800"
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="4fc26-103">Tutorial: Azure Active Directory integration with ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="4fc26-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="4fc26-104">In this tutorial, you learn how to integrate ADP Globalview with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4fc26-104">In this tutorial, you learn how to integrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4fc26-105">Integrating ADP Globalview with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4fc26-105">Integrating ADP Globalview with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4fc26-106">You can control in Azure AD who has access to ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="4fc26-106">You can control in Azure AD who has access to ADP Globalview</span></span>
- <span data-ttu-id="4fc26-107">You can enable your users to automatically get signed-on to ADP Globalview (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4fc26-107">You can enable your users to automatically get signed-on to ADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4fc26-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4fc26-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4fc26-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4fc26-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fc26-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4fc26-110">Prerequisites</span></span>

<span data-ttu-id="4fc26-111">To configure Azure AD integration with ADP Globalview, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4fc26-111">To configure Azure AD integration with ADP Globalview, you need the following items:</span></span>

- <span data-ttu-id="4fc26-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4fc26-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4fc26-113">An ADP Globalview single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4fc26-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4fc26-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4fc26-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4fc26-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4fc26-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4fc26-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4fc26-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4fc26-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4fc26-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4fc26-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4fc26-118">Scenario description</span></span>
<span data-ttu-id="4fc26-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4fc26-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4fc26-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4fc26-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4fc26-121">Adding ADP Globalview from the gallery</span><span class="sxs-lookup"><span data-stu-id="4fc26-121">Adding ADP Globalview from the gallery</span></span>
2. <span data-ttu-id="4fc26-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4fc26-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-the-gallery"></a><span data-ttu-id="4fc26-123">Adding ADP Globalview from the gallery</span><span class="sxs-lookup"><span data-stu-id="4fc26-123">Adding ADP Globalview from the gallery</span></span>
<span data-ttu-id="4fc26-124">To configure the integration of ADP Globalview into Azure AD, you need to add ADP Globalview from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4fc26-124">To configure the integration of ADP Globalview into Azure AD, you need to add ADP Globalview from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4fc26-125">**To add ADP Globalview from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4fc26-125">**To add ADP Globalview from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4fc26-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4fc26-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4fc26-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4fc26-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4fc26-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4fc26-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="4fc26-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="4fc26-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="4fc26-133">In the search box, type **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="4fc26-133">In the search box, type **ADP Globalview**.</span></span>

    ![Creating an Azure AD test user](./media/adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="4fc26-135">In the results panel, select **ADP Globalview**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4fc26-135">In the results panel, select **ADP Globalview**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4fc26-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4fc26-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4fc26-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="4fc26-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4fc26-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP Globalview is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fc26-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP Globalview is to a user in Azure AD.</span></span> <span data-ttu-id="4fc26-140">In other words, a link relationship between an Azure AD user and the related user in ADP Globalview needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4fc26-140">In other words, a link relationship between an Azure AD user and the related user in ADP Globalview needs to be established.</span></span>

<span data-ttu-id="4fc26-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="4fc26-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP Globalview.</span></span>

<span data-ttu-id="4fc26-142">To configure and test Azure AD single sign-on with ADP Globalview, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4fc26-142">To configure and test Azure AD single sign-on with ADP Globalview, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4fc26-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4fc26-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4fc26-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fc26-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4fc26-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - to have a counterpart of Britta Simon in ADP Globalview that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4fc26-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - to have a counterpart of Britta Simon in ADP Globalview that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4fc26-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4fc26-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4fc26-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4fc26-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4fc26-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4fc26-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4fc26-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP Globalview application.</span><span class="sxs-lookup"><span data-stu-id="4fc26-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="4fc26-150">**To configure Azure AD single sign-on with ADP Globalview, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4fc26-150">**To configure Azure AD single sign-on with ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="4fc26-151">In the Azure portal, on the **ADP Globalview** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4fc26-151">In the Azure portal, on the **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="4fc26-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4fc26-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="4fc26-155">On the **ADP Globalview Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4fc26-155">On the **ADP Globalview Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="4fc26-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span><span class="sxs-lookup"><span data-stu-id="4fc26-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4fc26-158">The value is not real.</span><span class="sxs-lookup"><span data-stu-id="4fc26-158">The value is not real.</span></span> <span data-ttu-id="4fc26-159">Update the value with the actual Identifier.</span><span class="sxs-lookup"><span data-stu-id="4fc26-159">Update the value with the actual Identifier.</span></span> <span data-ttu-id="4fc26-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to get the value.</span><span class="sxs-lookup"><span data-stu-id="4fc26-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to get the value.</span></span>
 
4. <span data-ttu-id="4fc26-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4fc26-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="4fc26-163">The ADP GlobalView application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="4fc26-163">The ADP GlobalView application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="4fc26-164">The following screenshot shows an example for it.</span><span class="sxs-lookup"><span data-stu-id="4fc26-164">The following screenshot shows an example for it.</span></span> <span data-ttu-id="4fc26-165">The claim names always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2, which contains the EmployeeID of the user.</span><span class="sxs-lookup"><span data-stu-id="4fc26-165">The claim names always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2, which contains the EmployeeID of the user.</span></span> <span data-ttu-id="4fc26-166">Here the user mapping from Azure AD to ADP GlobalView is done on the EmployeeID but you can map it to a different value also based on your application settings.</span><span class="sxs-lookup"><span data-stu-id="4fc26-166">Here the user mapping from Azure AD to ADP GlobalView is done on the EmployeeID but you can map it to a different value also based on your application settings.</span></span> <span data-ttu-id="4fc26-167">You can work with the ADP GlobalView team first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span><span class="sxs-lookup"><span data-stu-id="4fc26-167">You can work with the ADP GlobalView team first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="4fc26-168">You can also map the Email and UserID claim as shown in the picture.</span><span class="sxs-lookup"><span data-stu-id="4fc26-168">You can also map the Email and UserID claim as shown in the picture.</span></span>

    ![Configure Single Sign-On](./media/adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="4fc26-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4fc26-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="4fc26-171">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="4fc26-171">Attribute Name</span></span> | <span data-ttu-id="4fc26-172">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="4fc26-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="4fc26-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="4fc26-173">personalimmutableid</span></span> | <span data-ttu-id="4fc26-174">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="4fc26-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="4fc26-175">email</span><span class="sxs-lookup"><span data-stu-id="4fc26-175">email</span></span>               | <span data-ttu-id="4fc26-176">user.mail</span><span class="sxs-lookup"><span data-stu-id="4fc26-176">user.mail</span></span> |
    | <span data-ttu-id="4fc26-177">userid</span><span class="sxs-lookup"><span data-stu-id="4fc26-177">userid</span></span>              | <span data-ttu-id="4fc26-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="4fc26-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="4fc26-179">a.</span><span class="sxs-lookup"><span data-stu-id="4fc26-179">a.</span></span> <span data-ttu-id="4fc26-180">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="4fc26-180">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/adglobalview-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="4fc26-183">b.</span><span class="sxs-lookup"><span data-stu-id="4fc26-183">b.</span></span> <span data-ttu-id="4fc26-184">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="4fc26-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="4fc26-185">c.</span><span class="sxs-lookup"><span data-stu-id="4fc26-185">c.</span></span> <span data-ttu-id="4fc26-186">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="4fc26-186">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="4fc26-187">d.</span><span class="sxs-lookup"><span data-stu-id="4fc26-187">d.</span></span> <span data-ttu-id="4fc26-188">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="4fc26-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4fc26-189">Before you can configure the SAML assertion, you need to contact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span><span class="sxs-lookup"><span data-stu-id="4fc26-189">Before you can configure the SAML assertion, you need to contact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="4fc26-190">You need this value to configure the custom claim for your application.</span><span class="sxs-lookup"><span data-stu-id="4fc26-190">You need this value to configure the custom claim for your application.</span></span> 

8. <span data-ttu-id="4fc26-191">On the **ADP Globalview Configuration** section, click **Configure ADP Globalview** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="4fc26-191">On the **ADP Globalview Configuration** section, click **Configure ADP Globalview** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4fc26-192">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="4fc26-192">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="4fc26-194">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4fc26-194">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="4fc26-196">To configure single sign-on on **ADP Globalview** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="4fc26-196">To configure single sign-on on **ADP Globalview** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="4fc26-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="4fc26-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4fc26-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="4fc26-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4fc26-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4fc26-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4fc26-200">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4fc26-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="4fc26-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fc26-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="4fc26-203">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4fc26-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4fc26-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4fc26-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="4fc26-206">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4fc26-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4fc26-208">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="4fc26-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4fc26-210">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4fc26-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4fc26-212">a.</span><span class="sxs-lookup"><span data-stu-id="4fc26-212">a.</span></span> <span data-ttu-id="4fc26-213">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4fc26-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4fc26-214">b.</span><span class="sxs-lookup"><span data-stu-id="4fc26-214">b.</span></span> <span data-ttu-id="4fc26-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4fc26-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4fc26-216">c.</span><span class="sxs-lookup"><span data-stu-id="4fc26-216">c.</span></span> <span data-ttu-id="4fc26-217">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="4fc26-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4fc26-218">d.</span><span class="sxs-lookup"><span data-stu-id="4fc26-218">d.</span></span> <span data-ttu-id="4fc26-219">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4fc26-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="4fc26-220">Creating an ADP Globalview test user</span><span class="sxs-lookup"><span data-stu-id="4fc26-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="4fc26-221">The objective of this section is to create a user called Britta Simon in ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="4fc26-221">The objective of this section is to create a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="4fc26-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP GlobalView account.</span><span class="sxs-lookup"><span data-stu-id="4fc26-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP GlobalView account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4fc26-223">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4fc26-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4fc26-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="4fc26-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP Globalview.</span></span>

![Assign User][200] 

<span data-ttu-id="4fc26-226">**To assign Britta Simon to ADP Globalview, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4fc26-226">**To assign Britta Simon to ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="4fc26-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4fc26-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="4fc26-229">In the applications list, select **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="4fc26-229">In the applications list, select **ADP Globalview**.</span></span>

    ![Configure Single Sign-On](./media/adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="4fc26-231">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4fc26-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="4fc26-233">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4fc26-233">Click **Add** button.</span></span> <span data-ttu-id="4fc26-234">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4fc26-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="4fc26-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4fc26-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4fc26-237">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4fc26-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4fc26-238">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4fc26-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4fc26-239">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="4fc26-239">Testing single sign-on</span></span>

<span data-ttu-id="4fc26-240">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4fc26-240">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="4fc26-241">When you click the ADP GlobalView tile in the Access Panel, you should get automatically signed-on to your ADP GlobalView application.</span><span class="sxs-lookup"><span data-stu-id="4fc26-241">When you click the ADP GlobalView tile in the Access Panel, you should get automatically signed-on to your ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4fc26-242">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4fc26-242">Additional resources</span></span>

* [<span data-ttu-id="4fc26-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4fc26-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4fc26-244">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4fc26-244">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/adglobalview-tutorial/tutorial_general_203.png

