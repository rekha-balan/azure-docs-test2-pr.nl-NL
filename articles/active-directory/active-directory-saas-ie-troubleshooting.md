---
title: Troubleshooting the Azure Access Panel Extension for IE | Microsoft Docs
description: How to use group policy to deploy the Internet Explorer add-on for the My Apps portal.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: f56b3230-26fd-42ec-9e3d-2c12daf15479
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2250d71f5d20a9270b53b803f61e71c71a7cc2ed
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661162"
---
# <a name="troubleshooting-the-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="a6d33-103">Troubleshooting the Access Panel Extension for Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="a6d33-103">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="a6d33-104">This article helps you troubleshoot the following problems:</span><span class="sxs-lookup"><span data-stu-id="a6d33-104">This article helps you troubleshoot the following problems:</span></span>

* <span data-ttu-id="a6d33-105">You're unable to access your apps through the My Apps portal while using Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="a6d33-105">You're unable to access your apps through the My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="a6d33-106">You see the "Install Software" message even though you've already installed the software.</span><span class="sxs-lookup"><span data-stu-id="a6d33-106">You see the "Install Software" message even though you've already installed the software.</span></span>

<span data-ttu-id="a6d33-107">If you are an admin, see also: [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="a6d33-107">If you are an admin, see also: [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-the-diagnostic-tool"></a><span data-ttu-id="a6d33-108">Run the Diagnostic Tool</span><span class="sxs-lookup"><span data-stu-id="a6d33-108">Run the Diagnostic Tool</span></span>
<span data-ttu-id="a6d33-109">You can diagnose installation problems with the Access Panel Extension by downloading and running the Access Panel diagnostic tool:</span><span class="sxs-lookup"><span data-stu-id="a6d33-109">You can diagnose installation problems with the Access Panel Extension by downloading and running the Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="a6d33-110">Click here to download the diagnostic tool.</span><span class="sxs-lookup"><span data-stu-id="a6d33-110">Click here to download the diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="a6d33-111">Open the file, and press **Extract all** button.</span><span class="sxs-lookup"><span data-stu-id="a6d33-111">Open the file, and press **Extract all** button.</span></span>
   
    ![Press Extract All](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="a6d33-113">Then press the **Extract** button to continue.</span><span class="sxs-lookup"><span data-stu-id="a6d33-113">Then press the **Extract** button to continue.</span></span>
   
    ![Press Extract](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="a6d33-115">To run the tool, right-click the file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span><span class="sxs-lookup"><span data-stu-id="a6d33-115">To run the tool, right-click the file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Open with > Microsoft Windows Based Script Host](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="a6d33-117">You will then see the following diagnostic window, which describes what might be wrong with your installation.</span><span class="sxs-lookup"><span data-stu-id="a6d33-117">You will then see the following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![A sample of the diagnostic window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="a6d33-119">Click "**YES**" to let the program fix the issues that have been found.</span><span class="sxs-lookup"><span data-stu-id="a6d33-119">Click "**YES**" to let the program fix the issues that have been found.</span></span>
7. <span data-ttu-id="a6d33-120">To save these changes, close every Internet Explorer window, and then open Internet Explorer again.</span><span class="sxs-lookup"><span data-stu-id="a6d33-120">To save these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="a6d33-121">If you still can't access your apps, try the steps below.</span><span class="sxs-lookup"><span data-stu-id="a6d33-121">If you still can't access your apps, try the steps below.</span></span>

## <a name="check-that-the-access-panel-extension-is-enabled"></a><span data-ttu-id="a6d33-122">Check that the Access Panel Extension is enabled</span><span class="sxs-lookup"><span data-stu-id="a6d33-122">Check that the Access Panel Extension is enabled</span></span>
<span data-ttu-id="a6d33-123">To verify that the Access Panel Extension is enabled in Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="a6d33-123">To verify that the Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="a6d33-124">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span><span class="sxs-lookup"><span data-stu-id="a6d33-124">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="a6d33-125">Then select **Internet options**.</span><span class="sxs-lookup"><span data-stu-id="a6d33-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="a6d33-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span><span class="sxs-lookup"><span data-stu-id="a6d33-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Go to Tools > Internet Options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="a6d33-128">Click the **Programs** tab, then click the **Manage add-ons** button.</span><span class="sxs-lookup"><span data-stu-id="a6d33-128">Click the **Programs** tab, then click the **Manage add-ons** button.</span></span>
   
    ![Click Manage Add-Ons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="a6d33-130">In this dialog, select **Access Panel Extension** and then click the **Enable** button.</span><span class="sxs-lookup"><span data-stu-id="a6d33-130">In this dialog, select **Access Panel Extension** and then click the **Enable** button.</span></span>
   
    ![Click Enable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="a6d33-132">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span><span class="sxs-lookup"><span data-stu-id="a6d33-132">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="a6d33-133">Enable Extensions for InPrivate Browsing</span><span class="sxs-lookup"><span data-stu-id="a6d33-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="a6d33-134">If you are using the InPrivate Browsing mode:</span><span class="sxs-lookup"><span data-stu-id="a6d33-134">If you are using the InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="a6d33-135">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span><span class="sxs-lookup"><span data-stu-id="a6d33-135">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="a6d33-136">Then select **Internet options**.</span><span class="sxs-lookup"><span data-stu-id="a6d33-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="a6d33-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span><span class="sxs-lookup"><span data-stu-id="a6d33-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![A sample of the diagnostic window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="a6d33-139">Go to the **Privacy** tab, then **uncheck** the checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span><span class="sxs-lookup"><span data-stu-id="a6d33-139">Go to the **Privacy** tab, then **uncheck** the checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![Uncheck Disable toolbars and extensions when InPrivate Browsing starts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="a6d33-141">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span><span class="sxs-lookup"><span data-stu-id="a6d33-141">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-the-access-panel-extension"></a><span data-ttu-id="a6d33-142">Uninstall the Access Panel Extension</span><span class="sxs-lookup"><span data-stu-id="a6d33-142">Uninstall the Access Panel Extension</span></span>
<span data-ttu-id="a6d33-143">To uninstall the Access Panel extension from your computer:</span><span class="sxs-lookup"><span data-stu-id="a6d33-143">To uninstall the Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="a6d33-144">On your keyboard, press the **Windows key** to open the Start menu.</span><span class="sxs-lookup"><span data-stu-id="a6d33-144">On your keyboard, press the **Windows key** to open the Start menu.</span></span> <span data-ttu-id="a6d33-145">When the menu is open, you can type anything to do a search.</span><span class="sxs-lookup"><span data-stu-id="a6d33-145">When the menu is open, you can type anything to do a search.</span></span> <span data-ttu-id="a6d33-146">Type "Control Panel" and then open the **Control Panel** when it appears in the search results.</span><span class="sxs-lookup"><span data-stu-id="a6d33-146">Type "Control Panel" and then open the **Control Panel** when it appears in the search results.</span></span>
   
    ![Search for Control Panel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="a6d33-148">In the top right corner of the Control Panel, change the **View by** option to **Large icons**.</span><span class="sxs-lookup"><span data-stu-id="a6d33-148">In the top right corner of the Control Panel, change the **View by** option to **Large icons**.</span></span> <span data-ttu-id="a6d33-149">Then find and click the **Programs and Features** button.</span><span class="sxs-lookup"><span data-stu-id="a6d33-149">Then find and click the **Programs and Features** button.</span></span>
   
    ![Chang the view to show Large Icons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="a6d33-151">From the list, select **Access Panel Extension**, and the click the **Uninstall** button.</span><span class="sxs-lookup"><span data-stu-id="a6d33-151">From the list, select **Access Panel Extension**, and the click the **Uninstall** button.</span></span>
   
    ![Click Uninstall](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="a6d33-153">You can then try to install the extension again to see if the problem has been resolved.</span><span class="sxs-lookup"><span data-stu-id="a6d33-153">You can then try to install the extension again to see if the problem has been resolved.</span></span>

<span data-ttu-id="a6d33-154">If you encounter issues uninstalling the extension, you can also remove it using the [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span><span class="sxs-lookup"><span data-stu-id="a6d33-154">If you encounter issues uninstalling the extension, you can also remove it using the [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="a6d33-155">Related Articles</span><span class="sxs-lookup"><span data-stu-id="a6d33-155">Related Articles</span></span>
* [<span data-ttu-id="a6d33-156">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6d33-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="a6d33-157">Application access and single sign-on with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6d33-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a6d33-158">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span><span class="sxs-lookup"><span data-stu-id="a6d33-158">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)













