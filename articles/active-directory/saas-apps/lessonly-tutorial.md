---
title: 'Tutorial: Azure Active Directory integration with Lessonly.com | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Lessonly.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 8c9dc6e6-5d85-4553-8a35-c7137064b928
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 2a4bae196e956d92548944637509b23f78ceb5d2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869989"
---
# <a name="tutorial-azure-active-directory-integration-with-lessonlycom"></a><span data-ttu-id="978b9-103">Tutorial: Azure Active Directory integration with Lessonly.com</span><span class="sxs-lookup"><span data-stu-id="978b9-103">Tutorial: Azure Active Directory integration with Lessonly.com</span></span>

<span data-ttu-id="978b9-104">In this tutorial, you learn how to integrate Lessonly.com with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="978b9-104">In this tutorial, you learn how to integrate Lessonly.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="978b9-105">Integrating Lessonly.com with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="978b9-105">Integrating Lessonly.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="978b9-106">You can control in Azure AD who has access to Lessonly.com</span><span class="sxs-lookup"><span data-stu-id="978b9-106">You can control in Azure AD who has access to Lessonly.com</span></span>
- <span data-ttu-id="978b9-107">You can enable your users to automatically get signed-on to Lessonly.com (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="978b9-107">You can enable your users to automatically get signed-on to Lessonly.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="978b9-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="978b9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="978b9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="978b9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="978b9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="978b9-110">Prerequisites</span></span>

<span data-ttu-id="978b9-111">To configure Azure AD integration with Lessonly.com, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="978b9-111">To configure Azure AD integration with Lessonly.com, you need the following items:</span></span>

- <span data-ttu-id="978b9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="978b9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="978b9-113">A Lessonly.com single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="978b9-113">A Lessonly.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="978b9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="978b9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="978b9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="978b9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="978b9-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="978b9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="978b9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="978b9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="978b9-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="978b9-118">Scenario description</span></span>
<span data-ttu-id="978b9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="978b9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="978b9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="978b9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="978b9-121">Adding Lessonly.com from the gallery</span><span class="sxs-lookup"><span data-stu-id="978b9-121">Adding Lessonly.com from the gallery</span></span>
1. <span data-ttu-id="978b9-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="978b9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lessonlycom-from-the-gallery"></a><span data-ttu-id="978b9-123">Adding Lessonly.com from the gallery</span><span class="sxs-lookup"><span data-stu-id="978b9-123">Adding Lessonly.com from the gallery</span></span>
<span data-ttu-id="978b9-124">To configure the integration of Lessonly.com into Azure AD, you need to add Lessonly.com from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="978b9-124">To configure the integration of Lessonly.com into Azure AD, you need to add Lessonly.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="978b9-125">**To add Lessonly.com from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="978b9-125">**To add Lessonly.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="978b9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="978b9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="978b9-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="978b9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="978b9-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="978b9-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="978b9-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="978b9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="978b9-133">In the search box, type **Lessonly.com**.</span><span class="sxs-lookup"><span data-stu-id="978b9-133">In the search box, type **Lessonly.com**.</span></span>

    ![Creating an Azure AD test user](./media/lessonly-tutorial/tutorial_lessonly.com_search.png)

1. <span data-ttu-id="978b9-135">In the results panel, select **Lessonly.com**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="978b9-135">In the results panel, select **Lessonly.com**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/lessonly-tutorial/tutorial_lessonly.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="978b9-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="978b9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="978b9-138">In this section, you configure and test Azure AD single sign-on with Lessonly.com based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="978b9-138">In this section, you configure and test Azure AD single sign-on with Lessonly.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="978b9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lessonly.com is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="978b9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lessonly.com is to a user in Azure AD.</span></span> <span data-ttu-id="978b9-140">In other words, a link relationship between an Azure AD user and the related user in Lessonly.com needs to be established.</span><span class="sxs-lookup"><span data-stu-id="978b9-140">In other words, a link relationship between an Azure AD user and the related user in Lessonly.com needs to be established.</span></span>

<span data-ttu-id="978b9-141">In Lessonly.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="978b9-141">In Lessonly.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="978b9-142">To configure and test Azure AD single sign-on with Lessonly.com, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="978b9-142">To configure and test Azure AD single sign-on with Lessonly.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="978b9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="978b9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="978b9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="978b9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="978b9-145">**[Creating a Lessonly.com test user](#creating-a-lessonly-test-user)** - to have a counterpart of Britta Simon in Lessonly.com that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="978b9-145">**[Creating a Lessonly.com test user](#creating-a-lessonly-test-user)** - to have a counterpart of Britta Simon in Lessonly.com that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="978b9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="978b9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="978b9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="978b9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="978b9-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="978b9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="978b9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lessonly.com application.</span><span class="sxs-lookup"><span data-stu-id="978b9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lessonly.com application.</span></span>

<span data-ttu-id="978b9-150">**To configure Azure AD single sign-on with Lessonly.com, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="978b9-150">**To configure Azure AD single sign-on with Lessonly.com, perform the following steps:**</span></span>

1. <span data-ttu-id="978b9-151">In the Azure portal, on the **Lessonly.com** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="978b9-151">In the Azure portal, on the **Lessonly.com** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="978b9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="978b9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/lessonly-tutorial/tutorial_lessonly.com_samlbase.png)

1. <span data-ttu-id="978b9-155">On the **Lessonly.com Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="978b9-155">On the **Lessonly.com Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/lessonly-tutorial/tutorial_lessonly.com_url.png)

    <span data-ttu-id="978b9-157">a.</span><span class="sxs-lookup"><span data-stu-id="978b9-157">a.</span></span> <span data-ttu-id="978b9-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="978b9-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lessonly.com/signin`|

    >[!NOTE]
    ><span data-ttu-id="978b9-159">When referencing a generic name that **companyname** needs to be replaced by an actual name.</span><span class="sxs-lookup"><span data-stu-id="978b9-159">When referencing a generic name that **companyname** needs to be replaced by an actual name.</span></span>
    
    <span data-ttu-id="978b9-160">b.</span><span class="sxs-lookup"><span data-stu-id="978b9-160">b.</span></span> <span data-ttu-id="978b9-161">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="978b9-161">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lessonly.com/auth/saml/metadata`|

    > [!NOTE] 
    > <span data-ttu-id="978b9-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="978b9-162">These values are not real.</span></span> <span data-ttu-id="978b9-163">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="978b9-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="978b9-164">Contact [Lessonly.com Client support team](mailto:support@lessonly.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="978b9-164">Contact [Lessonly.com Client support team](mailto:support@lessonly.com) to get these values.</span></span> 

1. <span data-ttu-id="978b9-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="978b9-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/lessonly-tutorial/tutorial_lessonly.com_certificate.png)

1. <span data-ttu-id="978b9-167">The Lessonly.com application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="978b9-167">The Lessonly.com application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.The following screenshot shows an example for this.</span></span>

    ![Configure Single Sign-On](./media/lessonly-tutorial/tutorial_lessonly_06.png)
           
1. <span data-ttu-id="978b9-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="978b9-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>

    | <span data-ttu-id="978b9-170">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="978b9-170">Attribute Name</span></span>   | <span data-ttu-id="978b9-171">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="978b9-171">Attribute Value</span></span> |
    | ---------------  | ----------------|
    | <span data-ttu-id="978b9-172">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="978b9-172">urn:oid:2.5.4.42</span></span> |<span data-ttu-id="978b9-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="978b9-173">user.givenname</span></span> |
    | <span data-ttu-id="978b9-174">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="978b9-174">urn:oid:2.5.4.4</span></span>  |<span data-ttu-id="978b9-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="978b9-175">user.surname</span></span> |
    | <span data-ttu-id="978b9-176">urn:oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="978b9-176">urn:oid:0.9.2342.19200300.100.1.3</span></span> |<span data-ttu-id="978b9-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="978b9-177">user.mail</span></span> |
    | <span data-ttu-id="978b9-178">urn:oid:1.3.6.1.4.1.5923.1.1.1.10</span><span class="sxs-lookup"><span data-stu-id="978b9-178">urn:oid:1.3.6.1.4.1.5923.1.1.1.10</span></span> |<span data-ttu-id="978b9-179">user.objectid</span><span class="sxs-lookup"><span data-stu-id="978b9-179">user.objectid</span></span> |

    <span data-ttu-id="978b9-180">a.</span><span class="sxs-lookup"><span data-stu-id="978b9-180">a.</span></span> <span data-ttu-id="978b9-181">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="978b9-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/lessonly-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/lessonly-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="978b9-184">b.</span><span class="sxs-lookup"><span data-stu-id="978b9-184">b.</span></span> <span data-ttu-id="978b9-185">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="978b9-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="978b9-186">c.</span><span class="sxs-lookup"><span data-stu-id="978b9-186">c.</span></span> <span data-ttu-id="978b9-187">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="978b9-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="978b9-188">d.</span><span class="sxs-lookup"><span data-stu-id="978b9-188">d.</span></span> <span data-ttu-id="978b9-189">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="978b9-189">Click **Ok**.</span></span>     

1. <span data-ttu-id="978b9-190">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="978b9-190">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/lessonly-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="978b9-192">On the **Lessonly.com Configuration** section, click **Configure Lessonly.com** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="978b9-192">On the **Lessonly.com Configuration** section, click **Configure Lessonly.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="978b9-193">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="978b9-193">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/lessonly-tutorial/tutorial_lessonly.com_configure.png)

1. <span data-ttu-id="978b9-195">To configure single sign-on on **Lessonly.com** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Lessonly.com support team](mailto:support@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="978b9-195">To configure single sign-on on **Lessonly.com** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Lessonly.com support team](mailto:support@lessonly.com).</span></span>

> [!TIP]
> <span data-ttu-id="978b9-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="978b9-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="978b9-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="978b9-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="978b9-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="978b9-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="978b9-199">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="978b9-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="978b9-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="978b9-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="978b9-202">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="978b9-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="978b9-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="978b9-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/lessonly-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="978b9-205">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="978b9-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/lessonly-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="978b9-207">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="978b9-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/lessonly-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="978b9-209">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="978b9-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/lessonly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="978b9-211">a.</span><span class="sxs-lookup"><span data-stu-id="978b9-211">a.</span></span> <span data-ttu-id="978b9-212">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="978b9-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="978b9-213">b.</span><span class="sxs-lookup"><span data-stu-id="978b9-213">b.</span></span> <span data-ttu-id="978b9-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="978b9-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="978b9-215">c.</span><span class="sxs-lookup"><span data-stu-id="978b9-215">c.</span></span> <span data-ttu-id="978b9-216">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="978b9-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="978b9-217">d.</span><span class="sxs-lookup"><span data-stu-id="978b9-217">d.</span></span> <span data-ttu-id="978b9-218">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="978b9-218">Click **Create**.</span></span>
 
### <a name="creating-a-lessonlycom-test-user"></a><span data-ttu-id="978b9-219">Creating a Lessonly.com test user</span><span class="sxs-lookup"><span data-stu-id="978b9-219">Creating a Lessonly.com test user</span></span>

<span data-ttu-id="978b9-220">The objective of this section is to create a user called Britta Simon in Lessonly.com.</span><span class="sxs-lookup"><span data-stu-id="978b9-220">The objective of this section is to create a user called Britta Simon in Lessonly.com.</span></span> <span data-ttu-id="978b9-221">Lessonly.com supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="978b9-221">Lessonly.com supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="978b9-222">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="978b9-222">There is no action item for you in this section.</span></span> <span data-ttu-id="978b9-223">A new user will be created during an attempt to access Lessonly.com if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="978b9-223">A new user will be created during an attempt to access Lessonly.com if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="978b9-224">If you need to create an user manually, you need to contact the [Lessonly.com support team](mailto:support@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="978b9-224">If you need to create an user manually, you need to contact the [Lessonly.com support team](mailto:support@lessonly.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="978b9-225">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="978b9-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="978b9-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lessonly.com.</span><span class="sxs-lookup"><span data-stu-id="978b9-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lessonly.com.</span></span>

![Assign User][200] 

<span data-ttu-id="978b9-228">**To assign Britta Simon to Lessonly.com, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="978b9-228">**To assign Britta Simon to Lessonly.com, perform the following steps:**</span></span>

1. <span data-ttu-id="978b9-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="978b9-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="978b9-231">In the applications list, select **Lessonly.com**.</span><span class="sxs-lookup"><span data-stu-id="978b9-231">In the applications list, select **Lessonly.com**.</span></span>

    ![Configure Single Sign-On](./media/lessonly-tutorial/tutorial_lessonly.com_app.png)

1. <span data-ttu-id="978b9-233">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="978b9-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="978b9-235">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="978b9-235">Click **Add** button.</span></span> <span data-ttu-id="978b9-236">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="978b9-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="978b9-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="978b9-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="978b9-239">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="978b9-239">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="978b9-240">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="978b9-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="978b9-241">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="978b9-241">Testing single sign-on</span></span>

<span data-ttu-id="978b9-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="978b9-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="978b9-243">When you click the Lessonly.com tile in the Access Panel, you should get automatically signed-on to your Lessonly.com application.</span><span class="sxs-lookup"><span data-stu-id="978b9-243">When you click the Lessonly.com tile in the Access Panel, you should get automatically signed-on to your Lessonly.com application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="978b9-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="978b9-244">Additional resources</span></span>

* [<span data-ttu-id="978b9-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="978b9-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="978b9-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="978b9-246">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/lessonly-tutorial/tutorial_general_01.png
[2]: ./media/lessonly-tutorial/tutorial_general_02.png
[3]: ./media/lessonly-tutorial/tutorial_general_03.png
[4]: ./media/lessonly-tutorial/tutorial_general_04.png

[100]: ./media/lessonly-tutorial/tutorial_general_100.png

[200]: ./media/lessonly-tutorial/tutorial_general_200.png
[201]: ./media/lessonly-tutorial/tutorial_general_201.png
[202]: ./media/lessonly-tutorial/tutorial_general_202.png
[203]: ./media/lessonly-tutorial/tutorial_general_203.png

