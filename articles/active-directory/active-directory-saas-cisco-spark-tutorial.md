---
title: 'Tutorial: Azure Active Directory integration with Cisco Spark | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Cisco Spark.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: a1571f745e95021526c51607ccfd54435b0d9c39
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549371"
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="b15da-103">Tutorial: Azure Active Directory integration with Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="b15da-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>
<span data-ttu-id="b15da-104">In this tutorial, you learn how to integrate Cisco Spark with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b15da-104">In this tutorial, you learn how to integrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b15da-105">Integrating Cisco Spark with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b15da-105">Integrating Cisco Spark with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="b15da-106">You can control in Azure AD who has access to Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="b15da-106">You can control in Azure AD who has access to Cisco Spark</span></span>
* <span data-ttu-id="b15da-107">You can enable your users to automatically get signed-on to Cisco Spark single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="b15da-107">You can enable your users to automatically get signed-on to Cisco Spark single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="b15da-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="b15da-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="b15da-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b15da-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b15da-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b15da-110">Prerequisites</span></span>
<span data-ttu-id="b15da-111">To configure Azure AD integration with Cisco Spark, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b15da-111">To configure Azure AD integration with Cisco Spark, you need the following items:</span></span>

* <span data-ttu-id="b15da-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b15da-112">An Azure AD subscription</span></span>
* <span data-ttu-id="b15da-113">A **Cisco Spark** single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b15da-113">A **Cisco Spark** single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="b15da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b15da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="b15da-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b15da-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="b15da-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="b15da-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="b15da-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b15da-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b15da-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b15da-118">Scenario description</span></span>
<span data-ttu-id="b15da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b15da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b15da-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b15da-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b15da-121">Adding Cisco Spark from the gallery</span><span class="sxs-lookup"><span data-stu-id="b15da-121">Adding Cisco Spark from the gallery</span></span>
2. <span data-ttu-id="b15da-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="b15da-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cisco-spark-from-the-gallery"></a><span data-ttu-id="b15da-123">Add Cisco Spark from the gallery</span><span class="sxs-lookup"><span data-stu-id="b15da-123">Add Cisco Spark from the gallery</span></span>
<span data-ttu-id="b15da-124">To configure the integration of Cisco Spark into Azure AD, you need to add Cisco Spark from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b15da-124">To configure the integration of Cisco Spark into Azure AD, you need to add Cisco Spark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b15da-125">**To add Cisco Spark from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b15da-125">**To add Cisco Spark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b15da-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b15da-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="b15da-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="b15da-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b15da-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="b15da-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="b15da-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="b15da-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="b15da-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="b15da-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="b15da-135">In the search box, type **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="b15da-135">In the search box, type **Cisco Spark**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_01.png)
7. <span data-ttu-id="b15da-137">In the results pane, select **Cisco Spark**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="b15da-137">In the results pane, select **Cisco Spark**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="b15da-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="b15da-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="b15da-140">In this section, you configure and test Azure AD SSO with Cisco Spark based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b15da-140">In this section, you configure and test Azure AD SSO with Cisco Spark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b15da-141">For SSO to work, Azure AD needs to know what the counterpart user in Cisco Spark is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b15da-141">For SSO to work, Azure AD needs to know what the counterpart user in Cisco Spark is to a user in Azure AD.</span></span> <span data-ttu-id="b15da-142">In other words, a link relationship between an Azure AD user and the related user in Cisco Spark needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b15da-142">In other words, a link relationship between an Azure AD user and the related user in Cisco Spark needs to be established.</span></span>

<span data-ttu-id="b15da-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="b15da-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Cisco Spark.</span></span> <span data-ttu-id="b15da-144">To configure and test Azure AD single sign-on with Cisco Spark, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b15da-144">To configure and test Azure AD single sign-on with Cisco Spark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b15da-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b15da-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b15da-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b15da-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b15da-147">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - to have a counterpart of Britta Simon in Cisco Spark that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="b15da-147">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - to have a counterpart of Britta Simon in Cisco Spark that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b15da-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b15da-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b15da-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b15da-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="b15da-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="b15da-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="b15da-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your Cisco Spark application.</span><span class="sxs-lookup"><span data-stu-id="b15da-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="b15da-152">Cisco Spark application expects the SAML assertions to contain specific attributes.</span><span class="sxs-lookup"><span data-stu-id="b15da-152">Cisco Spark application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="b15da-153">Configure the following attributes  for this application.</span><span class="sxs-lookup"><span data-stu-id="b15da-153">Configure the following attributes  for this application.</span></span> <span data-ttu-id="b15da-154">You can manage the values of these attributes from the **"Atrributes"** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="b15da-154">You can manage the values of these attributes from the **"Atrributes"** tab of the application.</span></span> <span data-ttu-id="b15da-155">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="b15da-155">The following screenshot shows an example for this.</span></span>

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_03.png) 

<span data-ttu-id="b15da-157">**To configure Azure AD SSO with Cisco Spark, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b15da-157">**To configure Azure AD SSO with Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="b15da-158">In the Azure classic portal, on the **Cisco Spark** application integration page, in the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="b15da-158">In the Azure classic portal, on the **Cisco Spark** application integration page, in the menu on the top, click **Attributes**.</span></span>
   
    ![Configure Single Sign-On][5]
2. <span data-ttu-id="b15da-160">On the **SAML token attributes** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b15da-160">On the **SAML token attributes** dialog, perform the following steps:</span></span>
  1. <span data-ttu-id="b15da-161">Click **add user attribute** to open the **Add User Attribure** dialog.</span><span class="sxs-lookup"><span data-stu-id="b15da-161">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_05.png)
  2. <span data-ttu-id="b15da-163">In the **Attribute Name** textbox, type **uid**.</span><span class="sxs-lookup"><span data-stu-id="b15da-163">In the **Attribute Name** textbox, type **uid**.</span></span>
  3. <span data-ttu-id="b15da-164">From the **Attribute Value** list, select **user.userprincipal**.</span><span class="sxs-lookup"><span data-stu-id="b15da-164">From the **Attribute Value** list, select **user.userprincipal**.</span></span>
  4. <span data-ttu-id="b15da-165">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b15da-165">Click **Complete**.</span></span> <span data-ttu-id="b15da-166">Then, **Apply Changes** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="b15da-166">Then, **Apply Changes** at the bottom of the page.</span></span>
3. <span data-ttu-id="b15da-167">In the menu on the top, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="b15da-167">In the menu on the top, click **Quick Start**.</span></span>
   
    ![Configure Single Sign-On][6]
4. <span data-ttu-id="b15da-169">In the classic portal, on the **Cisco Spark** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="b15da-169">In the classic portal, on the **Cisco Spark** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][7] 
5. <span data-ttu-id="b15da-171">On the **How would you like users to sign on to Cisco Spark** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b15da-171">On the **How would you like users to sign on to Cisco Spark** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_06.png)
6. <span data-ttu-id="b15da-173">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b15da-173">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_07.png)
  1. <span data-ttu-id="b15da-175">In the Sign On URL textbox, type a URL using the following pattern: `https://web.ciscospark.com/#/signin`.</span><span class="sxs-lookup"><span data-stu-id="b15da-175">In the Sign On URL textbox, type a URL using the following pattern: `https://web.ciscospark.com/#/signin`.</span></span>
  2. <span data-ttu-id="b15da-176">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b15da-176">Click **Next**.</span></span>
7. <span data-ttu-id="b15da-177">On the **Configure single sign-on at Cisco Spark** page, Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b15da-177">On the **Configure single sign-on at Cisco Spark** page, Click **Download metadata**, and then save the file on your computer.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_09.png)
8. <span data-ttu-id="b15da-179">Sign in to [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="b15da-179">Sign in to [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>
9. <span data-ttu-id="b15da-180">Select **Settings** and under the **Authentication** section, click **Modify**.</span><span class="sxs-lookup"><span data-stu-id="b15da-180">Select **Settings** and under the **Authentication** section, click **Modify**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
9. <span data-ttu-id="b15da-182">Select **Integrate a 3rd-party identity provider. (Advanced)** and go to the next screen.</span><span class="sxs-lookup"><span data-stu-id="b15da-182">Select **Integrate a 3rd-party identity provider. (Advanced)** and go to the next screen.</span></span>
10. <span data-ttu-id="b15da-183">Click on **Download Metadata File** and save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b15da-183">Click on **Download Metadata File** and save the file on your computer.</span></span>
11. <span data-ttu-id="b15da-184">On the **Import Idp Metadata** page, either drag and drop the Azure AD metadata file onto the page or use the file browser option to locate and upload the Azure AD metadata file.</span><span class="sxs-lookup"><span data-stu-id="b15da-184">On the **Import Idp Metadata** page, either drag and drop the Azure AD metadata file onto the page or use the file browser option to locate and upload the Azure AD metadata file.</span></span> <span data-ttu-id="b15da-185">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b15da-185">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)
12. <span data-ttu-id="b15da-187">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span><span class="sxs-lookup"><span data-stu-id="b15da-187">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>
13. <span data-ttu-id="b15da-188">Return to the **Cisco Cloud Collaboration Management** browser tab. If the test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b15da-188">Return to the **Cisco Cloud Collaboration Management** browser tab. If the test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>
14. <span data-ttu-id="b15da-189">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b15da-189">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
15. <span data-ttu-id="b15da-191">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b15da-191">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
     ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b15da-193">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b15da-193">Create an Azure AD test user</span></span>
<span data-ttu-id="b15da-194">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b15da-194">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="b15da-196">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b15da-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b15da-197">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b15da-197">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="b15da-199">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="b15da-199">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b15da-200">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="b15da-200">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="b15da-202">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="b15da-202">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="b15da-204">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b15da-204">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="b15da-206">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="b15da-206">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="b15da-207">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b15da-207">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="b15da-208">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b15da-208">Click **Next**.</span></span>
6. <span data-ttu-id="b15da-209">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b15da-209">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="b15da-211">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b15da-211">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="b15da-212">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b15da-212">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="b15da-213">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b15da-213">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="b15da-214">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="b15da-214">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="b15da-215">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b15da-215">Click **Next**.</span></span>
7. <span data-ttu-id="b15da-216">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="b15da-216">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="b15da-218">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b15da-218">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="b15da-220">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="b15da-220">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="b15da-221">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b15da-221">Click **Complete**.</span></span>   

### <a name="create-a-cisco-spark-test-user"></a><span data-ttu-id="b15da-222">Create a Cisco Spark test user</span><span class="sxs-lookup"><span data-stu-id="b15da-222">Create a Cisco Spark test user</span></span>
<span data-ttu-id="b15da-223">In this section, you create a user called Britta Simon in Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="b15da-223">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="b15da-224">In this section, you create a user called Britta Simon in Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="b15da-224">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="b15da-225">Go to the [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="b15da-225">Go to the [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>
2. <span data-ttu-id="b15da-226">Click on **Users** and then **Manage Users**.</span><span class="sxs-lookup"><span data-stu-id="b15da-226">Click on **Users** and then **Manage Users**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 
3. <span data-ttu-id="b15da-228">In the **Manage User** window, select **Manually add or modify users** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b15da-228">In the **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>
4. <span data-ttu-id="b15da-229">Select **Names and Email address**.</span><span class="sxs-lookup"><span data-stu-id="b15da-229">Select **Names and Email address**.</span></span> <span data-ttu-id="b15da-230">Then, fill out the textbox as follow:</span><span class="sxs-lookup"><span data-stu-id="b15da-230">Then, fill out the textbox as follow:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
  1. <span data-ttu-id="b15da-232">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b15da-232">In the **First Name** textbox, type **Britta**.</span></span> 
  2. <span data-ttu-id="b15da-233">In the **Last Name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b15da-233">In the **Last Name** textbox, type **Simon**.</span></span>
  3. <span data-ttu-id="b15da-234">In the **Email address** textbox, type **britta.simon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="b15da-234">In the **Email address** textbox, type **britta.simon@contoso.com**.</span></span>
5. <span data-ttu-id="b15da-235">Click on the plus sign to add Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b15da-235">Click on the plus sign to add Britta Simon.</span></span> <span data-ttu-id="b15da-236">Then, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b15da-236">Then, click **Next**.</span></span>
6. <span data-ttu-id="b15da-237">In the **Add Services for Users** window, click **Save** and then **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b15da-237">In the **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b15da-238">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b15da-238">Assign the Azure AD test user</span></span>
<span data-ttu-id="b15da-239">In this section, you enable Britta Simon to use Azure SSO by granting her access to Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="b15da-239">In this section, you enable Britta Simon to use Azure SSO by granting her access to Cisco Spark.</span></span>

![Assign User][200] 

<span data-ttu-id="b15da-241">**To assign Britta Simon to Cisco Spark, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b15da-241">**To assign Britta Simon to Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="b15da-242">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="b15da-242">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="b15da-244">In the applications list, select **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="b15da-244">In the applications list, select **Cisco Spark**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_14.png) 
3. <span data-ttu-id="b15da-246">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="b15da-246">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="b15da-248">In the All Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b15da-248">In the All Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="b15da-249">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="b15da-249">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="b15da-251">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="b15da-251">Test single sign-on</span></span>
<span data-ttu-id="b15da-252">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b15da-252">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="b15da-253">When you click the Cisco Spark tile in the Access Panel, you should get automatically signed-on to your Cisco Spark application.</span><span class="sxs-lookup"><span data-stu-id="b15da-253">When you click the Cisco Spark tile in the Access Panel, you should get automatically signed-on to your Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b15da-254">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b15da-254">Additional resources</span></span>
* [<span data-ttu-id="b15da-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b15da-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b15da-256">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b15da-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png


[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_general_05.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_general_06.png
[7]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_general_050.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_general_070.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cisco-spark-tutorial/tutorial_general_205.png

































