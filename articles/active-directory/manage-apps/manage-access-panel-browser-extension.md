---
title: Troubleshooting the Azure Access Panel Extension for IE | Microsoft Docs
description: How to use group policy to deploy the Internet Explorer add-on for the My Apps portal.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/30/2018
ms.author: barbkess
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b13b5a7d5366a0bce97d8e735dbf3822186d21cb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856807"
---
# <a name="troubleshooting-the-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="c4368-103">Troubleshooting the Access Panel Extension for Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="c4368-103">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="c4368-104">This article helps you troubleshoot the following problems:</span><span class="sxs-lookup"><span data-stu-id="c4368-104">This article helps you troubleshoot the following problems:</span></span>

* <span data-ttu-id="c4368-105">You're unable to access your apps through the My Apps portal while using Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="c4368-105">You're unable to access your apps through the My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="c4368-106">You see the "Install Software" message even though you've already installed the software.</span><span class="sxs-lookup"><span data-stu-id="c4368-106">You see the "Install Software" message even though you've already installed the software.</span></span>

<span data-ttu-id="c4368-107">If you are an admin, see also: [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](deploy-access-panel-browser-extension.md)</span><span class="sxs-lookup"><span data-stu-id="c4368-107">If you are an admin, see also: [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](deploy-access-panel-browser-extension.md)</span></span>

## <a name="run-the-diagnostic-tool"></a><span data-ttu-id="c4368-108">Run the Diagnostic Tool</span><span class="sxs-lookup"><span data-stu-id="c4368-108">Run the Diagnostic Tool</span></span>
<span data-ttu-id="c4368-109">You can diagnose installation problems with the Access Panel Extension by downloading and running the Access Panel diagnostic tool:</span><span class="sxs-lookup"><span data-stu-id="c4368-109">You can diagnose installation problems with the Access Panel Extension by downloading and running the Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="c4368-110">Click here to download the diagnostic tool.</span><span class="sxs-lookup"><span data-stu-id="c4368-110">Click here to download the diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="c4368-111">Open the file, and press **Extract all** button.</span><span class="sxs-lookup"><span data-stu-id="c4368-111">Open the file, and press **Extract all** button.</span></span>
   
    ![Press Extract All](./media/manage-access-panel-browser-extension/extract1.png)
3. <span data-ttu-id="c4368-113">Then press the **Extract** button to continue.</span><span class="sxs-lookup"><span data-stu-id="c4368-113">Then press the **Extract** button to continue.</span></span>
   
    ![Press Extract](./media/manage-access-panel-browser-extension/extract2.png)
4. <span data-ttu-id="c4368-115">To run the tool, right-click the file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span><span class="sxs-lookup"><span data-stu-id="c4368-115">To run the tool, right-click the file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Open with > Microsoft Windows Based Script Host](./media/manage-access-panel-browser-extension/open_tool.png)
5. <span data-ttu-id="c4368-117">You will then see the following diagnostic window, which describes what might be wrong with your installation.</span><span class="sxs-lookup"><span data-stu-id="c4368-117">You will then see the following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![A sample of the diagnostic window](./media/manage-access-panel-browser-extension/tool_preview.png)
6. <span data-ttu-id="c4368-119">Click "**YES**" to let the program fix the issues that have been found.</span><span class="sxs-lookup"><span data-stu-id="c4368-119">Click "**YES**" to let the program fix the issues that have been found.</span></span>
7. <span data-ttu-id="c4368-120">To save these changes, close every Internet Explorer window, and then open Internet Explorer again.</span><span class="sxs-lookup"><span data-stu-id="c4368-120">To save these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="c4368-121">If you still can't access your apps, try the steps below.</span><span class="sxs-lookup"><span data-stu-id="c4368-121">If you still can't access your apps, try the steps below.</span></span>

## <a name="check-that-the-access-panel-extension-is-enabled"></a><span data-ttu-id="c4368-122">Check that the Access Panel Extension is enabled</span><span class="sxs-lookup"><span data-stu-id="c4368-122">Check that the Access Panel Extension is enabled</span></span>
<span data-ttu-id="c4368-123">To verify that the Access Panel Extension is enabled in Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="c4368-123">To verify that the Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="c4368-124">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span><span class="sxs-lookup"><span data-stu-id="c4368-124">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="c4368-125">Then select **Internet options**.</span><span class="sxs-lookup"><span data-stu-id="c4368-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="c4368-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span><span class="sxs-lookup"><span data-stu-id="c4368-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Go to Tools > Internet Options](./media/manage-access-panel-browser-extension/internetoptions.png)
2. <span data-ttu-id="c4368-128">Click the **Programs** tab, then click the **Manage add-ons** button.</span><span class="sxs-lookup"><span data-stu-id="c4368-128">Click the **Programs** tab, then click the **Manage add-ons** button.</span></span>
   
    ![Click Manage Add-Ons](./media/manage-access-panel-browser-extension/internetoptions_programs.png)
3. <span data-ttu-id="c4368-130">In this dialog, select **Access Panel Extension** and then click the **Enable** button.</span><span class="sxs-lookup"><span data-stu-id="c4368-130">In this dialog, select **Access Panel Extension** and then click the **Enable** button.</span></span>
   
    ![Click Enable](./media/manage-access-panel-browser-extension/enableaddon.png)
4. <span data-ttu-id="c4368-132">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span><span class="sxs-lookup"><span data-stu-id="c4368-132">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="c4368-133">Enable Extensions for InPrivate Browsing</span><span class="sxs-lookup"><span data-stu-id="c4368-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="c4368-134">If you are using the InPrivate Browsing mode:</span><span class="sxs-lookup"><span data-stu-id="c4368-134">If you are using the InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="c4368-135">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span><span class="sxs-lookup"><span data-stu-id="c4368-135">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="c4368-136">Then select **Internet options**.</span><span class="sxs-lookup"><span data-stu-id="c4368-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="c4368-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span><span class="sxs-lookup"><span data-stu-id="c4368-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![A sample of the diagnostic window](./media/manage-access-panel-browser-extension/inprivateoptions.png)
2. <span data-ttu-id="c4368-139">Go to the **Privacy** tab, then **uncheck** the checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span><span class="sxs-lookup"><span data-stu-id="c4368-139">Go to the **Privacy** tab, then **uncheck** the checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![Uncheck Disable toolbars and extensions when InPrivate Browsing starts](./media/manage-access-panel-browser-extension/enabletoolbars.png)
3. <span data-ttu-id="c4368-141">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span><span class="sxs-lookup"><span data-stu-id="c4368-141">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-the-access-panel-extension"></a><span data-ttu-id="c4368-142">Uninstall the Access Panel Extension</span><span class="sxs-lookup"><span data-stu-id="c4368-142">Uninstall the Access Panel Extension</span></span>
<span data-ttu-id="c4368-143">To uninstall the Access Panel extension from your computer:</span><span class="sxs-lookup"><span data-stu-id="c4368-143">To uninstall the Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="c4368-144">On your keyboard, press the **Windows key** to open the Start menu.</span><span class="sxs-lookup"><span data-stu-id="c4368-144">On your keyboard, press the **Windows key** to open the Start menu.</span></span> <span data-ttu-id="c4368-145">When the menu is open, you can type anything to do a search.</span><span class="sxs-lookup"><span data-stu-id="c4368-145">When the menu is open, you can type anything to do a search.</span></span> <span data-ttu-id="c4368-146">Type "Control Panel" and then open the **Control Panel** when it appears in the search results.</span><span class="sxs-lookup"><span data-stu-id="c4368-146">Type "Control Panel" and then open the **Control Panel** when it appears in the search results.</span></span>
   
    ![Search for Control Panel](./media/manage-access-panel-browser-extension/search_sm.png)
2. <span data-ttu-id="c4368-148">In the top right corner of the Control Panel, change the **View by** option to **Large icons**.</span><span class="sxs-lookup"><span data-stu-id="c4368-148">In the top right corner of the Control Panel, change the **View by** option to **Large icons**.</span></span> <span data-ttu-id="c4368-149">Then find and click the **Programs and Features** button.</span><span class="sxs-lookup"><span data-stu-id="c4368-149">Then find and click the **Programs and Features** button.</span></span>
   
    ![Chang the view to show Large Icons](./media/manage-access-panel-browser-extension/control_panel.png)
3. <span data-ttu-id="c4368-151">From the list, select **Access Panel Extension**, and the click the **Uninstall** button.</span><span class="sxs-lookup"><span data-stu-id="c4368-151">From the list, select **Access Panel Extension**, and the click the **Uninstall** button.</span></span>
   
    ![Click Uninstall](./media/manage-access-panel-browser-extension/uninstall.png)
4. <span data-ttu-id="c4368-153">You can then try to install the extension again to see if the problem has been resolved.</span><span class="sxs-lookup"><span data-stu-id="c4368-153">You can then try to install the extension again to see if the problem has been resolved.</span></span>

<span data-ttu-id="c4368-154">If you encounter issues uninstalling the extension, you can also remove it using the [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span><span class="sxs-lookup"><span data-stu-id="c4368-154">If you encounter issues uninstalling the extension, you can also remove it using the [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="c4368-155">Related Articles</span><span class="sxs-lookup"><span data-stu-id="c4368-155">Related Articles</span></span>
* [<span data-ttu-id="c4368-156">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4368-156">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="c4368-157">Application access and single sign-on with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4368-157">Application access and single sign-on with Azure Active Directory</span></span>](what-is-single-sign-on.md)
* [<span data-ttu-id="c4368-158">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span><span class="sxs-lookup"><span data-stu-id="c4368-158">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>](deploy-access-panel-browser-extension.md)

