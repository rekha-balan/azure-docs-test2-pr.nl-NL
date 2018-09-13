---
title: 'Tutorial: Azure Active Directory integration with Cisco Spark | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Cisco Spark.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: bebc8d674d7448ea0ce6a1f11b7ae80335df9cdc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870000"
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="ed0cb-103">Tutorial: Azure Active Directory integration with Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="ed0cb-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="ed0cb-104">In this tutorial, you learn how to integrate Cisco Spark with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ed0cb-104">In this tutorial, you learn how to integrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ed0cb-105">Integrating Cisco Spark with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ed0cb-105">Integrating Cisco Spark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ed0cb-106">You can control in Azure AD who has access to Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="ed0cb-106">You can control in Azure AD who has access to Cisco Spark</span></span>
- <span data-ttu-id="ed0cb-107">You can enable your users to automatically get signed-on to Cisco Spark (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="ed0cb-107">You can enable your users to automatically get signed-on to Cisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ed0cb-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ed0cb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ed0cb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="ed0cb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed0cb-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ed0cb-110">Prerequisites</span></span>

<span data-ttu-id="ed0cb-111">To configure Azure AD integration with Cisco Spark, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ed0cb-111">To configure Azure AD integration with Cisco Spark, you need the following items:</span></span>

- <span data-ttu-id="ed0cb-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ed0cb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ed0cb-113">A Cisco Spark single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ed0cb-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ed0cb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ed0cb-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ed0cb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ed0cb-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ed0cb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ed0cb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ed0cb-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="ed0cb-118">Scenario description</span></span>
<span data-ttu-id="ed0cb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ed0cb-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ed0cb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ed0cb-121">Adding Cisco Spark from the gallery</span><span class="sxs-lookup"><span data-stu-id="ed0cb-121">Adding Cisco Spark from the gallery</span></span>
1. <span data-ttu-id="ed0cb-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ed0cb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-the-gallery"></a><span data-ttu-id="ed0cb-123">Adding Cisco Spark from the gallery</span><span class="sxs-lookup"><span data-stu-id="ed0cb-123">Adding Cisco Spark from the gallery</span></span>
<span data-ttu-id="ed0cb-124">To configure the integration of Cisco Spark into Azure AD, you need to add Cisco Spark from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-124">To configure the integration of Cisco Spark into Azure AD, you need to add Cisco Spark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ed0cb-125">**To add Cisco Spark from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ed0cb-125">**To add Cisco Spark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ed0cb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="ed0cb-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ed0cb-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="ed0cb-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="ed0cb-133">In the search box, type **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-133">In the search box, type **Cisco Spark**.</span></span>

    ![Creating an Azure AD test user](./media/cisco-spark-tutorial/tutorial_ciscospark_search.png)

1. <span data-ttu-id="ed0cb-135">In the results panel, select **Cisco Spark**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-135">In the results panel, select **Cisco Spark**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ed0cb-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ed0cb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ed0cb-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="ed0cb-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ed0cb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cisco Spark is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cisco Spark is to a user in Azure AD.</span></span> <span data-ttu-id="ed0cb-140">In other words, a link relationship between an Azure AD user and the related user in Cisco Spark needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-140">In other words, a link relationship between an Azure AD user and the related user in Cisco Spark needs to be established.</span></span>

<span data-ttu-id="ed0cb-141">In Cisco Spark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-141">In Cisco Spark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ed0cb-142">To configure and test Azure AD single sign-on with Cisco Spark, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ed0cb-142">To configure and test Azure AD single sign-on with Cisco Spark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ed0cb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="ed0cb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="ed0cb-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - to have a counterpart of Britta Simon in Cisco Spark that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - to have a counterpart of Britta Simon in Cisco Spark that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="ed0cb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="ed0cb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ed0cb-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ed0cb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ed0cb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cisco Spark application.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="ed0cb-150">**To configure Azure AD single sign-on with Cisco Spark, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ed0cb-150">**To configure Azure AD single sign-on with Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="ed0cb-151">In the Azure portal, on the **Cisco Spark** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-151">In the Azure portal, on the **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="ed0cb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

1. <span data-ttu-id="ed0cb-155">On the **Cisco Spark Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ed0cb-155">On the **Cisco Spark Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="ed0cb-157">a.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-157">a.</span></span> <span data-ttu-id="ed0cb-158">In the **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="ed0cb-158">In the **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="ed0cb-159">b.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-159">b.</span></span> <span data-ttu-id="ed0cb-160">In the **Identifier** textbox, type a URL using the following pattern: `https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="ed0cb-160">In the **Identifier** textbox, type a URL using the following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ed0cb-161">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-161">This value is not real.</span></span> <span data-ttu-id="ed0cb-162">Update this value with the actual Identifier.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-162">Update this value with the actual Identifier.</span></span> <span data-ttu-id="ed0cb-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) to get this value.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) to get this value.</span></span> 
 
1. <span data-ttu-id="ed0cb-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

1. <span data-ttu-id="ed0cb-166">Cisco Spark application expects the SAML assertions to contain specific attributes.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-166">Cisco Spark application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="ed0cb-167">Configure the following attributes  for this application.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="ed0cb-168">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-168">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="ed0cb-169">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-169">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_ciscospark_07.png) 

1. <span data-ttu-id="ed0cb-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ed0cb-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="ed0cb-172">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="ed0cb-172">Attribute Name</span></span>  | <span data-ttu-id="ed0cb-173">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="ed0cb-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="ed0cb-174">uid</span><span class="sxs-lookup"><span data-stu-id="ed0cb-174">uid</span></span>    | <span data-ttu-id="ed0cb-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="ed0cb-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="ed0cb-176">a.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-176">a.</span></span> <span data-ttu-id="ed0cb-177">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="ed0cb-180">b.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-180">b.</span></span> <span data-ttu-id="ed0cb-181">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="ed0cb-182">c.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-182">c.</span></span> <span data-ttu-id="ed0cb-183">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ed0cb-184">d.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-184">d.</span></span> <span data-ttu-id="ed0cb-185">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-185">Click **Ok**.</span></span>

1. <span data-ttu-id="ed0cb-186">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-186">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="ed0cb-188">Sign in to [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-188">Sign in to [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

1. <span data-ttu-id="ed0cb-189">Select **Settings** and under the **Authentication** section, click **Modify**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-189">Select **Settings** and under the **Authentication** section, click **Modify**.</span></span>
   
    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
1. <span data-ttu-id="ed0cb-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go to the next screen.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go to the next screen.</span></span>

1. <span data-ttu-id="ed0cb-192">On the **Import Idp Metadata** page, either drag and drop the Azure AD metadata file onto the page or use the file browser option to locate and upload the Azure AD metadata file.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-192">On the **Import Idp Metadata** page, either drag and drop the Azure AD metadata file onto the page or use the file browser option to locate and upload the Azure AD metadata file.</span></span> <span data-ttu-id="ed0cb-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_cisco_spark_11.png)

1. <span data-ttu-id="ed0cb-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

1. <span data-ttu-id="ed0cb-196">Return to the **Cisco Cloud Collaboration Management** browser tab. If the test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-196">Return to the **Cisco Cloud Collaboration Management** browser tab. If the test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="ed0cb-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="ed0cb-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ed0cb-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ed0cb-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ed0cb-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ed0cb-200">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ed0cb-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="ed0cb-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="ed0cb-203">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ed0cb-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ed0cb-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/cisco-spark-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="ed0cb-206">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/cisco-spark-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="ed0cb-208">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/cisco-spark-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="ed0cb-210">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ed0cb-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ed0cb-212">a.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-212">a.</span></span> <span data-ttu-id="ed0cb-213">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ed0cb-214">b.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-214">b.</span></span> <span data-ttu-id="ed0cb-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ed0cb-216">c.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-216">c.</span></span> <span data-ttu-id="ed0cb-217">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ed0cb-218">d.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-218">d.</span></span> <span data-ttu-id="ed0cb-219">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-219">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="ed0cb-220">Creating a Cisco Spark test user</span><span class="sxs-lookup"><span data-stu-id="ed0cb-220">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="ed0cb-221">In this section, you create a user called Britta Simon in Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-221">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="ed0cb-222">In this section, you create a user called Britta Simon in Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="ed0cb-223">Go to the [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-223">Go to the [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

1. <span data-ttu-id="ed0cb-224">Click **Users** and then **Manage Users**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-224">Click **Users** and then **Manage Users**.</span></span>
   
    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

1. <span data-ttu-id="ed0cb-226">In the **Manage User** window, select **Manually add or modify users** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-226">In the **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

1. <span data-ttu-id="ed0cb-227">Select **Names and Email address**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-227">Select **Names and Email address**.</span></span> <span data-ttu-id="ed0cb-228">Then, fill out the textbox as follows:</span><span class="sxs-lookup"><span data-stu-id="ed0cb-228">Then, fill out the textbox as follows:</span></span>
   
    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="ed0cb-230">a.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-230">a.</span></span> <span data-ttu-id="ed0cb-231">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-231">In the **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="ed0cb-232">b.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-232">b.</span></span> <span data-ttu-id="ed0cb-233">In the **Last Name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-233">In the **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="ed0cb-234">c.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-234">c.</span></span> <span data-ttu-id="ed0cb-235">In the **Email address** textbox, type **britta.simon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-235">In the **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

1. <span data-ttu-id="ed0cb-236">Click the plus sign to add Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-236">Click the plus sign to add Britta Simon.</span></span> <span data-ttu-id="ed0cb-237">Then, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-237">Then, click **Next**.</span></span>

1. <span data-ttu-id="ed0cb-238">In the **Add Services for Users** window, click **Save** and then **Finish**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-238">In the **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ed0cb-239">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ed0cb-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ed0cb-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cisco Spark.</span></span>

![Assign User][200] 

<span data-ttu-id="ed0cb-242">**To assign Britta Simon to Cisco Spark, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ed0cb-242">**To assign Britta Simon to Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="ed0cb-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="ed0cb-245">In the applications list, select **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-245">In the applications list, select **Cisco Spark**.</span></span>

    ![Configure Single Sign-On](./media/cisco-spark-tutorial/tutorial_ciscospark_app.png) 

1. <span data-ttu-id="ed0cb-247">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="ed0cb-249">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-249">Click **Add** button.</span></span> <span data-ttu-id="ed0cb-250">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="ed0cb-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="ed0cb-253">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-253">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="ed0cb-254">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ed0cb-255">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="ed0cb-255">Testing single sign-on</span></span>

<span data-ttu-id="ed0cb-256">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-256">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="ed0cb-257">When you click the Cisco Spark tile in the Access Panel, you should get automatically signed-on to your Cisco Spark application.</span><span class="sxs-lookup"><span data-stu-id="ed0cb-257">When you click the Cisco Spark tile in the Access Panel, you should get automatically signed-on to your Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ed0cb-258">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ed0cb-258">Additional resources</span></span>

* [<span data-ttu-id="ed0cb-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed0cb-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="ed0cb-260">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ed0cb-260">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/cisco-spark-tutorial/tutorial_general_203.png

