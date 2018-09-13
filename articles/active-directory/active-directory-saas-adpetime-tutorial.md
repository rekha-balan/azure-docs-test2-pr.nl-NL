---
title: 'Tutorial: Azure Active Directory integration with ADP eTime | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ADP eTime.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 342ba03125545ade050cf844e903faa4a5d84acb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550403"
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="99e5b-103">Tutorial: Azure Active Directory integration with ADP eTime</span><span class="sxs-lookup"><span data-stu-id="99e5b-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>
<span data-ttu-id="99e5b-104">The objective of this tutorial is to show you how to integrate ADP eTime with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="99e5b-104">The objective of this tutorial is to show you how to integrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="99e5b-105">Integrating ADP eTime with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="99e5b-105">Integrating ADP eTime with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="99e5b-106">You can control in Azure AD who has access to ADP eTime</span><span class="sxs-lookup"><span data-stu-id="99e5b-106">You can control in Azure AD who has access to ADP eTime</span></span>
* <span data-ttu-id="99e5b-107">You can enable your users to automatically get signed-on to ADP eTime single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="99e5b-107">You can enable your users to automatically get signed-on to ADP eTime single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="99e5b-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="99e5b-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="99e5b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="99e5b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99e5b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="99e5b-110">Prerequisites</span></span>
<span data-ttu-id="99e5b-111">To configure Azure AD integration with ADP eTime, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="99e5b-111">To configure Azure AD integration with ADP eTime, you need the following items:</span></span>

* <span data-ttu-id="99e5b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="99e5b-112">An Azure AD subscription</span></span>
* <span data-ttu-id="99e5b-113">A ADP eTime SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="99e5b-113">A ADP eTime SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="99e5b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="99e5b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="99e5b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="99e5b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="99e5b-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="99e5b-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="99e5b-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99e5b-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="99e5b-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="99e5b-118">Scenario Description</span></span>
<span data-ttu-id="99e5b-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="99e5b-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="99e5b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="99e5b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="99e5b-121">Adding ADP eTime from the gallery</span><span class="sxs-lookup"><span data-stu-id="99e5b-121">Adding ADP eTime from the gallery</span></span>
2. <span data-ttu-id="99e5b-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="99e5b-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-adp-etime-from-the-gallery"></a><span data-ttu-id="99e5b-123">Add ADP eTime from the gallery</span><span class="sxs-lookup"><span data-stu-id="99e5b-123">Add ADP eTime from the gallery</span></span>
<span data-ttu-id="99e5b-124">To configure the integration of ADP eTime into Azure AD, you need to add ADP eTime from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="99e5b-124">To configure the integration of ADP eTime into Azure AD, you need to add ADP eTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="99e5b-125">**To add ADP eTime from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99e5b-125">**To add ADP eTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="99e5b-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="99e5b-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="99e5b-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="99e5b-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="99e5b-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="99e5b-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="99e5b-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="99e5b-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="99e5b-135">In the search box, type **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-135">In the search box, type **ADP eTime**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_01.png)
7. <span data-ttu-id="99e5b-137">In the results pane, select **ADP eTime**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="99e5b-137">In the results pane, select **ADP eTime**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_06.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="99e5b-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="99e5b-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="99e5b-140">The objective of this section is to show you how to configure and test Azure AD SSO with ADP eTime based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="99e5b-140">The objective of this section is to show you how to configure and test Azure AD SSO with ADP eTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="99e5b-141">For SSO to work, Azure AD needs to know what the counterpart user in ADP eTime to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="99e5b-141">For SSO to work, Azure AD needs to know what the counterpart user in ADP eTime to an user in Azure AD is.</span></span> <span data-ttu-id="99e5b-142">In other words, a link relationship between an Azure AD user and the related user in ADP eTime needs to be established.</span><span class="sxs-lookup"><span data-stu-id="99e5b-142">In other words, a link relationship between an Azure AD user and the related user in ADP eTime needs to be established.</span></span>  

<span data-ttu-id="99e5b-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="99e5b-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP eTime.</span></span>

<span data-ttu-id="99e5b-144">To configure and test Azure AD SSO with ADP eTime, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="99e5b-144">To configure and test Azure AD SSO with ADP eTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="99e5b-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="99e5b-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="99e5b-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99e5b-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="99e5b-147">**[Creating a ADP eTime test user](#creating-a-adpetime-test-user)** - to have a counterpart of Britta Simon in ADP eTime that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="99e5b-147">**[Creating a ADP eTime test user](#creating-a-adpetime-test-user)** - to have a counterpart of Britta Simon in ADP eTime that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="99e5b-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="99e5b-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="99e5b-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="99e5b-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="99e5b-150">Configuring Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="99e5b-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="99e5b-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your ADP eTime application.</span><span class="sxs-lookup"><span data-stu-id="99e5b-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="99e5b-152">Your ADP eTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="99e5b-152">Your ADP eTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="99e5b-153">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="99e5b-153">The following screenshot shows an example for this.</span></span> <span data-ttu-id="99e5b-154">The claim name will always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2 which contains the EmployeeID of the user.</span><span class="sxs-lookup"><span data-stu-id="99e5b-154">The claim name will always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2 which contains the EmployeeID of the user.</span></span> 

<span data-ttu-id="99e5b-155">Here the user mapping fron Azure AD to ADP eTime will be done on the EmployeeID but you can map this to a different value also based on your application settings.</span><span class="sxs-lookup"><span data-stu-id="99e5b-155">Here the user mapping fron Azure AD to ADP eTime will be done on the EmployeeID but you can map this to a different value also based on your application settings.</span></span> <span data-ttu-id="99e5b-156">So please work with ADP eTime team first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span><span class="sxs-lookup"><span data-stu-id="99e5b-156">So please work with ADP eTime team first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span>  

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_02.png) 

<span data-ttu-id="99e5b-158">Before you can configure the SAML assertion, you need to contact your ADP eTime support team and request the value of the unique identifier attribute for your tenant.</span><span class="sxs-lookup"><span data-stu-id="99e5b-158">Before you can configure the SAML assertion, you need to contact your ADP eTime support team and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="99e5b-159">You need this value to configure the custom claim for your application.</span><span class="sxs-lookup"><span data-stu-id="99e5b-159">You need this value to configure the custom claim for your application.</span></span>

<span data-ttu-id="99e5b-160">**To configure Azure AD single sign-on with ADP eTime, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99e5b-160">**To configure Azure AD single sign-on with ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="99e5b-161">In the Azure classic portal, on the **ADP eTime** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="99e5b-161">In the Azure classic portal, on the **ADP eTime** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="99e5b-163">On the **How would you like users to sign on to ADP eTime** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-163">On the **How would you like users to sign on to ADP eTime** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_03.png) 
3. <span data-ttu-id="99e5b-165">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="99e5b-165">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_04.png) 
  1. <span data-ttu-id="99e5b-167">In the **Reply URL** textbox, type the URL used by your users to sign-on to your ADP eTime application using the following pattern: `https://<server name>.adp.com/affwebservices/public/saml2assertionconsumer`.</span><span class="sxs-lookup"><span data-stu-id="99e5b-167">In the **Reply URL** textbox, type the URL used by your users to sign-on to your ADP eTime application using the following pattern: `https://<server name>.adp.com/affwebservices/public/saml2assertionconsumer`.</span></span>
  2. <span data-ttu-id="99e5b-168">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-168">Click **Next**.</span></span>
4. <span data-ttu-id="99e5b-169">On the **Configure single sign-on at ADP eTime** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99e5b-169">On the **Configure single sign-on at ADP eTime** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_05.png)  
  1. <span data-ttu-id="99e5b-171">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="99e5b-171">Click **Download metadata**, and then save the file on your computer.</span></span> 
  2. <span data-ttu-id="99e5b-172">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-172">Click **Next**.</span></span>
2. <span data-ttu-id="99e5b-173">To get SSO configured for your application, contact your ADP eTime support team and email the attach downloaded metadata file, so that they can be configured for SSO integration.</span><span class="sxs-lookup"><span data-stu-id="99e5b-173">To get SSO configured for your application, contact your ADP eTime support team and email the attach downloaded metadata file, so that they can be configured for SSO integration.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="99e5b-174">After **ADP eTime** team configure the instance, get the **RelayState** value from them.Follow the below mentioned steps to configure it.</span><span class="sxs-lookup"><span data-stu-id="99e5b-174">After **ADP eTime** team configure the instance, get the **RelayState** value from them.Follow the below mentioned steps to configure it.</span></span> <span data-ttu-id="99e5b-175">After this configuration you can test the integration.</span><span class="sxs-lookup"><span data-stu-id="99e5b-175">After this configuration you can test the integration.</span></span> <span data-ttu-id="99e5b-176">So please note that this is important configuration for this application integration to work.</span><span class="sxs-lookup"><span data-stu-id="99e5b-176">So please note that this is important configuration for this application integration to work.</span></span>
   >  
6. <span data-ttu-id="99e5b-177">To configure the RelayState value in Azure AD, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99e5b-177">To configure the RelayState value in Azure AD, perform the following steps:</span></span> 
  1. <span data-ttu-id="99e5b-178">Logon to the [Azure Management Portal](https://portal.azure.com) as administrator.</span><span class="sxs-lookup"><span data-stu-id="99e5b-178">Logon to the [Azure Management Portal](https://portal.azure.com) as administrator.</span></span>
  2. <span data-ttu-id="99e5b-179">In the left navigation pane, click **More Services**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-179">In the left navigation pane, click **More Services**.</span></span>  

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_07.png) 
 3. <span data-ttu-id="99e5b-181">In the **Search** textbox, type **Azure Active Directory**, and then click the related link.</span><span class="sxs-lookup"><span data-stu-id="99e5b-181">In the **Search** textbox, type **Azure Active Directory**, and then click the related link.</span></span> 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_08.png)   
 4. <span data-ttu-id="99e5b-183">Click **Enterprise Applications**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-183">Click **Enterprise Applications**.</span></span> 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_09.png)  
 5. <span data-ttu-id="99e5b-185">In the **Manage** section, click **All Applications**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-185">In the **Manage** section, click **All Applications**.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_10.png) 
 6. <span data-ttu-id="99e5b-187">In the **Search** textbox, type **ADP eTime**, and then click the related link.</span><span class="sxs-lookup"><span data-stu-id="99e5b-187">In the **Search** textbox, type **ADP eTime**, and then click the related link.</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_11.png)  
 7. <span data-ttu-id="99e5b-189">In the **Manage** section, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-189">In the **Manage** section, click **Single sign-on**.</span></span> 
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_12.png) 
 8. <span data-ttu-id="99e5b-191">Select **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-191">Select **Show advanced URL settings**.</span></span>
 
     ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_13.png) 
 9. <span data-ttu-id="99e5b-193">In the **Relay State** textbox, type a value using the following patterns, and then save the settings:</span><span class="sxs-lookup"><span data-stu-id="99e5b-193">In the **Relay State** textbox, type a value using the following patterns, and then save the settings:</span></span> 
 
    * <span data-ttu-id="99e5b-194">Production environment: `https://fed.adp.com/saml/fedlanding.html?<id>`</span><span class="sxs-lookup"><span data-stu-id="99e5b-194">Production environment: `https://fed.adp.com/saml/fedlanding.html?<id>`</span></span> 
    * <span data-ttu-id="99e5b-195">Staging environment: `https://fed-stag.adp.com/saml/fedlanding.html?PORTAL`</span><span class="sxs-lookup"><span data-stu-id="99e5b-195">Staging environment: `https://fed-stag.adp.com/saml/fedlanding.html?PORTAL`</span></span>
     
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_14.png) 

4. <span data-ttu-id="99e5b-197">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-197">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
 
 ![Azure AD Single Sign-On][10]
5. <span data-ttu-id="99e5b-199">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-199">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
 ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="99e5b-201">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="99e5b-201">Create an Azure AD test user</span></span>
<span data-ttu-id="99e5b-202">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99e5b-202">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

* <span data-ttu-id="99e5b-203">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-203">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="99e5b-205">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99e5b-205">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="99e5b-206">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-206">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="99e5b-208">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="99e5b-208">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="99e5b-209">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-209">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="99e5b-211">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-211">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="99e5b-213">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99e5b-213">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="99e5b-215">As **Type Of User**, select **New user in your organization**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-215">As **Type Of User**, select **New user in your organization**.</span></span>
 2. <span data-ttu-id="99e5b-216">In the **User Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-216">In the **User Name** textbox, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="99e5b-217">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-217">Click **Next**.</span></span>
6. <span data-ttu-id="99e5b-218">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99e5b-218">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="99e5b-220">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-220">In the **First Name** textbox, type **Britta**.</span></span>   
 2. <span data-ttu-id="99e5b-221">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-221">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="99e5b-222">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-222">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="99e5b-223">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-223">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="99e5b-224">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-224">Click **Next**.</span></span>
7. <span data-ttu-id="99e5b-225">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-225">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="99e5b-227">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99e5b-227">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="99e5b-229">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-229">Write down the value of the **New Password**.</span></span>
 2. <span data-ttu-id="99e5b-230">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-230">Click **Complete**.</span></span>   

### <a name="create-a-adp-etime-test-user"></a><span data-ttu-id="99e5b-231">Create a ADP eTime test user</span><span class="sxs-lookup"><span data-stu-id="99e5b-231">Create a ADP eTime test user</span></span>
<span data-ttu-id="99e5b-232">The objective of this section is to create a user called Britta Simon in ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="99e5b-232">The objective of this section is to create a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="99e5b-233">Please work with ADP eTime support team to add the users in the ADP eTime account.</span><span class="sxs-lookup"><span data-stu-id="99e5b-233">Please work with ADP eTime support team to add the users in the ADP eTime account.</span></span> 

>[!NOTE]
><span data-ttu-id="99e5b-234">If you need to create an user manually, you need to contact the ADP eTime support team.</span><span class="sxs-lookup"><span data-stu-id="99e5b-234">If you need to create an user manually, you need to contact the ADP eTime support team.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="99e5b-235">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="99e5b-235">Assign the Azure AD test user</span></span>
<span data-ttu-id="99e5b-236">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="99e5b-236">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to ADP eTime.</span></span>

![Assign User][200] 

<span data-ttu-id="99e5b-238">**To assign Britta Simon to ADP eTime, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="99e5b-238">**To assign Britta Simon to ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="99e5b-239">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="99e5b-239">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="99e5b-241">In the applications list, select **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-241">In the applications list, select **ADP eTime**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_50.png) 
3. <span data-ttu-id="99e5b-243">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-243">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="99e5b-245">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-245">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="99e5b-246">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="99e5b-246">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="99e5b-248">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="99e5b-248">Test single sign-on</span></span>
<span data-ttu-id="99e5b-249">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="99e5b-249">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="99e5b-250">When you click the ADP eTime tile in the Access Panel, you should get automatically signed-on to your ADP eTime application.</span><span class="sxs-lookup"><span data-stu-id="99e5b-250">When you click the ADP eTime tile in the Access Panel, you should get automatically signed-on to your ADP eTime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="99e5b-251">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="99e5b-251">Additional Resources</span></span>
* [<span data-ttu-id="99e5b-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99e5b-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="99e5b-253">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="99e5b-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_205.png


































