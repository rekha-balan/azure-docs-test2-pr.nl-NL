---
title: 'Tutorial: Azure Active Directory integration with Lifesize Cloud | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Lifesize Cloud.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: jeedes
ms.openlocfilehash: 519dda7e82e3032681bd20ac20235a7c5219cd94
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661578"
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="8978a-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="8978a-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>
<span data-ttu-id="8978a-104">In this tutorial, you learn how to integrate Lifesize Cloud with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8978a-104">In this tutorial, you learn how to integrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8978a-105">Integrating Lifesize Cloud with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8978a-105">Integrating Lifesize Cloud with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="8978a-106">You can control in Azure AD who has access to Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="8978a-106">You can control in Azure AD who has access to Lifesize Cloud</span></span>
* <span data-ttu-id="8978a-107">You can enable your users to automatically get signed-on to Lifesize Cloud single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="8978a-107">You can enable your users to automatically get signed-on to Lifesize Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="8978a-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="8978a-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="8978a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8978a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8978a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8978a-110">Prerequisites</span></span>
<span data-ttu-id="8978a-111">To configure Azure AD integration with Lifesize Cloud, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8978a-111">To configure Azure AD integration with Lifesize Cloud, you need the following items:</span></span>

* <span data-ttu-id="8978a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8978a-112">An Azure AD subscription</span></span>
* <span data-ttu-id="8978a-113">A Lifesize Cloud single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8978a-113">A Lifesize Cloud single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="8978a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8978a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="8978a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8978a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="8978a-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="8978a-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="8978a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8978a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8978a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8978a-118">Scenario description</span></span>
<span data-ttu-id="8978a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8978a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="8978a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8978a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="8978a-121">Adding Lifesize Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="8978a-121">Adding Lifesize Cloud from the gallery</span></span>
* <span data-ttu-id="8978a-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="8978a-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-lifesize-cloud-from-the-gallery"></a><span data-ttu-id="8978a-123">Add Lifesize Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="8978a-123">Add Lifesize Cloud from the gallery</span></span>
<span data-ttu-id="8978a-124">To configure the integration of Lifesize Cloud into Azure AD, you need to add Lifesize Cloud from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8978a-124">To configure the integration of Lifesize Cloud into Azure AD, you need to add Lifesize Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8978a-125">**To add Lifesize Cloud from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8978a-125">**To add Lifesize Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8978a-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8978a-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="8978a-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="8978a-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8978a-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="8978a-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="8978a-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="8978a-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="8978a-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="8978a-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="8978a-135">In the search box, type **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="8978a-135">In the search box, type **Lifesize Cloud**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_01.png)
7. <span data-ttu-id="8978a-137">In the results pane, select **Lifesize Cloud**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="8978a-137">In the results pane, select **Lifesize Cloud**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_02.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8978a-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8978a-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="8978a-140">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8978a-140">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8978a-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Lifesize Cloud is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8978a-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Lifesize Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="8978a-142">In other words, a link relationship between an Azure AD user and the related user in Lifesize Cloud needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8978a-142">In other words, a link relationship between an Azure AD user and the related user in Lifesize Cloud needs to be established.</span></span>

<span data-ttu-id="8978a-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="8978a-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lifesize Cloud.</span></span>

<span data-ttu-id="8978a-144">To configure and test Azure AD single sign-on with Lifesize Cloud, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8978a-144">To configure and test Azure AD single sign-on with Lifesize Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8978a-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8978a-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8978a-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8978a-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8978a-147">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - to have a counterpart of Britta Simon in Lifesize Cloud that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="8978a-147">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - to have a counterpart of Britta Simon in Lifesize Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="8978a-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8978a-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8978a-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8978a-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8978a-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8978a-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="8978a-151">In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your Lifesize Cloud application.</span><span class="sxs-lookup"><span data-stu-id="8978a-151">In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="8978a-152">**To configure Azure AD single sign-on with Lifesize Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8978a-152">**To configure Azure AD single sign-on with Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="8978a-153">In the classic portal, on the **Lifesize Cloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="8978a-153">In the classic portal, on the **Lifesize Cloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="8978a-155">On the **How would you like users to sign on to Lifesize Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8978a-155">On the **How would you like users to sign on to Lifesize Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_03.png) 
3. <span data-ttu-id="8978a-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8978a-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_04.png)   
  1. <span data-ttu-id="8978a-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Lifesize Cloud application using the following pattern: **https://login.lifesizecloud.com/ls/?acs**.</span><span class="sxs-lookup"><span data-stu-id="8978a-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Lifesize Cloud application using the following pattern: **https://login.lifesizecloud.com/ls/?acs**.</span></span>
  2. <span data-ttu-id="8978a-160">click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8978a-160">click **Next**.</span></span>
4. <span data-ttu-id="8978a-161">On the **Configure single sign-on at Lifesize Cloud** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8978a-161">On the **Configure single sign-on at Lifesize Cloud** page, perform the following steps:</span></span>
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_05.png)
   1. <span data-ttu-id="8978a-163">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8978a-163">Click **Download certificate**, and then save the file on your computer.</span></span>
   2. <span data-ttu-id="8978a-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8978a-164">Click **Next**.</span></span>
5. <span data-ttu-id="8978a-165">To get SSO configured for your application, login into the Lifesize Cloud application with Admin privileges.</span><span class="sxs-lookup"><span data-stu-id="8978a-165">To get SSO configured for your application, login into the Lifesize Cloud application with Admin privileges.</span></span>
6. <span data-ttu-id="8978a-166">In the top right corner click on your name and then click on the **Advance Settings**.</span><span class="sxs-lookup"><span data-stu-id="8978a-166">In the top right corner click on your name and then click on the **Advance Settings**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)
7. <span data-ttu-id="8978a-168">In the Advance Settings now click on the **SSO Configuration** link.</span><span class="sxs-lookup"><span data-stu-id="8978a-168">In the Advance Settings now click on the **SSO Configuration** link.</span></span> <span data-ttu-id="8978a-169">This will open the SSO Configuration page for your instance.</span><span class="sxs-lookup"><span data-stu-id="8978a-169">This will open the SSO Configuration page for your instance.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)
8. <span data-ttu-id="8978a-171">Now configure the following values in the SSO configuration UI.</span><span class="sxs-lookup"><span data-stu-id="8978a-171">Now configure the following values in the SSO configuration UI.</span></span>    
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
  1. <span data-ttu-id="8978a-173">Copy the value of Issuer URL from Azure AD and paste that in **Identity Provider Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="8978a-173">Copy the value of Issuer URL from Azure AD and paste that in **Identity Provider Issuer** textbox.</span></span> 
  2. <span data-ttu-id="8978a-174">Copy the value of Remote Login URL from Azure AD and paste that in **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="8978a-174">Copy the value of Remote Login URL from Azure AD and paste that in **Login URL** textbox.</span></span>   
  3. <span data-ttu-id="8978a-175">Open the downloaded certificate in notepad and copy the content of certificate, excluding the Begin Certificate and End Certificate lines, paste this in the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="8978a-175">Open the downloaded certificate in notepad and copy the content of certificate, excluding the Begin Certificate and End Certificate lines, paste this in the **X.509 Certificate** textbox.</span></span>
  4. <span data-ttu-id="8978a-176">In the SAML Attribute mapping for the **First Name** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="8978a-176">In the SAML Attribute mapping for the **First Name** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
  5. <span data-ttu-id="8978a-177">In the SAML Attribute mapping for the **Last Name** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="8978a-177">In the SAML Attribute mapping for the **Last Name** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
  6. <span data-ttu-id="8978a-178">In the SAML Attribute mapping for the **Email** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="8978a-178">In the SAML Attribute mapping for the **Email** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>
9. <span data-ttu-id="8978a-179">To check the configuration you can click on the **Test** button.</span><span class="sxs-lookup"><span data-stu-id="8978a-179">To check the configuration you can click on the **Test** button.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="8978a-180">For successful testing you need to complete the configuration wizard in Azure AD and also provide access to users or groups who can perform the test.</span><span class="sxs-lookup"><span data-stu-id="8978a-180">For successful testing you need to complete the configuration wizard in Azure AD and also provide access to users or groups who can perform the test.</span></span>
   >  
10. <span data-ttu-id="8978a-181">Enable the SSO by checking on the **Enable SSO** button.</span><span class="sxs-lookup"><span data-stu-id="8978a-181">Enable the SSO by checking on the **Enable SSO** button.</span></span>
11. <span data-ttu-id="8978a-182">Now click on the **Update** button so that all the settings are saved.</span><span class="sxs-lookup"><span data-stu-id="8978a-182">Now click on the **Update** button so that all the settings are saved.</span></span> <span data-ttu-id="8978a-183">This will generate the RelayState value.</span><span class="sxs-lookup"><span data-stu-id="8978a-183">This will generate the RelayState value.</span></span> <span data-ttu-id="8978a-184">Copy the RelayState value which is generated in the text box.</span><span class="sxs-lookup"><span data-stu-id="8978a-184">Copy the RelayState value which is generated in the text box.</span></span> <span data-ttu-id="8978a-185">We will need this value in the next steps.</span><span class="sxs-lookup"><span data-stu-id="8978a-185">We will need this value in the next steps.</span></span>
12. <span data-ttu-id="8978a-186">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8978a-186">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
   ![Azure AD Single Sign-On][10]
13. <span data-ttu-id="8978a-188">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8978a-188">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD Single Sign-On][11]
    
<span data-ttu-id="8978a-190">**To login to the Azure Management Portal:**</span><span class="sxs-lookup"><span data-stu-id="8978a-190">**To login to the Azure Management Portal:**</span></span>

1. <span data-ttu-id="8978a-191">Login into **https://portal.azure.com** using admin credentials.</span><span class="sxs-lookup"><span data-stu-id="8978a-191">Login into **https://portal.azure.com** using admin credentials.</span></span>
2. <span data-ttu-id="8978a-192">Click on **More Services** link in the left navigation pane.</span><span class="sxs-lookup"><span data-stu-id="8978a-192">Click on **More Services** link in the left navigation pane.</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_09.png)
3. <span data-ttu-id="8978a-194">Search for Azure Active Directory and Click on the **Azure Active Directory** Link.</span><span class="sxs-lookup"><span data-stu-id="8978a-194">Search for Azure Active Directory and Click on the **Azure Active Directory** Link.</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_10.png)
4. <span data-ttu-id="8978a-196">You will find all your SaaS applications under the **Enterprise Applications** button.</span><span class="sxs-lookup"><span data-stu-id="8978a-196">You will find all your SaaS applications under the **Enterprise Applications** button.</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_11.png)
5. <span data-ttu-id="8978a-198">Now click on **All Applications** link in the next blade.</span><span class="sxs-lookup"><span data-stu-id="8978a-198">Now click on **All Applications** link in the next blade.</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_12.png)
6. <span data-ttu-id="8978a-200">Search for Lifesize application for which you want to setup the RelayState.</span><span class="sxs-lookup"><span data-stu-id="8978a-200">Search for Lifesize application for which you want to setup the RelayState.</span></span> 
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_13.png)
7. <span data-ttu-id="8978a-202">Now Click **Single sign-on** link in the blade.</span><span class="sxs-lookup"><span data-stu-id="8978a-202">Now Click **Single sign-on** link in the blade.</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_14.png)
8. <span data-ttu-id="8978a-204">You will see the **Show advanced URL settings** check box.</span><span class="sxs-lookup"><span data-stu-id="8978a-204">You will see the **Show advanced URL settings** check box.</span></span> <span data-ttu-id="8978a-205">Click the check box.</span><span class="sxs-lookup"><span data-stu-id="8978a-205">Click the check box.</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_15.png)
9. <span data-ttu-id="8978a-207">Now configure the RelayState for the application, which you see in the Lifesize application SSO configuration page.</span><span class="sxs-lookup"><span data-stu-id="8978a-207">Now configure the RelayState for the application, which you see in the Lifesize application SSO configuration page.</span></span> 
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_16.png)
10. <span data-ttu-id="8978a-209">Save the settings.</span><span class="sxs-lookup"><span data-stu-id="8978a-209">Save the settings.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8978a-210">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8978a-210">Create an Azure AD test user</span></span>
<span data-ttu-id="8978a-211">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8978a-211">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="8978a-213">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8978a-213">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8978a-214">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8978a-214">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="8978a-216">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="8978a-216">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8978a-217">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="8978a-217">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="8978a-219">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="8978a-219">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="8978a-221">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8978a-221">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_05.png) 
   1. <span data-ttu-id="8978a-223">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="8978a-223">As Type Of User, select New user in your organization.</span></span>
   2. <span data-ttu-id="8978a-224">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8978a-224">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   3. <span data-ttu-id="8978a-225">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8978a-225">Click **Next**.</span></span>
6. <span data-ttu-id="8978a-226">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8978a-226">On the **User Profile** dialog page, perform the following steps:</span></span>

   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_06.png) 
   1. <span data-ttu-id="8978a-228">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8978a-228">In the **First Name** textbox, type **Britta**.</span></span>   
   2. <span data-ttu-id="8978a-229">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8978a-229">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="8978a-230">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8978a-230">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="8978a-231">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="8978a-231">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="8978a-232">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8978a-232">Click **Next**.</span></span>
7. <span data-ttu-id="8978a-233">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="8978a-233">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="8978a-235">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8978a-235">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_08.png) 
    1. <span data-ttu-id="8978a-237">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="8978a-237">Write down the value of the **New Password**.</span></span>
    2. <span data-ttu-id="8978a-238">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8978a-238">Click **Complete**.</span></span>   

### <a name="create-an-lifesize-cloud-test-user"></a><span data-ttu-id="8978a-239">Create an Lifesize Cloud test user</span><span class="sxs-lookup"><span data-stu-id="8978a-239">Create an Lifesize Cloud test user</span></span>
<span data-ttu-id="8978a-240">In this section, you create a user called Britta Simon in Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="8978a-240">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="8978a-241">Lifesize cloud does support automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="8978a-241">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="8978a-242">After successful authentication at Azure AD, the user will be automatically provisioned in the application.</span><span class="sxs-lookup"><span data-stu-id="8978a-242">After successful authentication at Azure AD, the user will be automatically provisioned in the application.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8978a-243">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8978a-243">Assign the Azure AD test user</span></span>
<span data-ttu-id="8978a-244">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="8978a-244">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Lifesize Cloud.</span></span>

![Assign User][200] 

<span data-ttu-id="8978a-246">**To assign Britta Simon to Lifesize Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8978a-246">**To assign Britta Simon to Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="8978a-247">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="8978a-247">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="8978a-249">In the applications list, select **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="8978a-249">In the applications list, select **Lifesize Cloud**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_50.png) 
3. <span data-ttu-id="8978a-251">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="8978a-251">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="8978a-253">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8978a-253">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="8978a-254">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="8978a-254">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="8978a-256">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="8978a-256">Test single sign-on</span></span>
<span data-ttu-id="8978a-257">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8978a-257">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8978a-258">When you click the Lifesize Cloud tile in the Access Panel, you should get automatically signed-on to your Lifesize Cloud application.</span><span class="sxs-lookup"><span data-stu-id="8978a-258">When you click the Lifesize Cloud tile in the Access Panel, you should get automatically signed-on to your Lifesize Cloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8978a-259">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8978a-259">Additional resources</span></span>
* [<span data-ttu-id="8978a-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8978a-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8978a-261">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8978a-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_205.png




































