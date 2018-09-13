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
# <a name="troubleshooting-the-access-panel-extension-for-internet-explorer"></a>Troubleshooting the Access Panel Extension for Internet Explorer
This article helps you troubleshoot the following problems:

* You're unable to access your apps through the My Apps portal while using Internet Explorer.
* You see the "Install Software" message even though you've already installed the software.

If you are an admin, see also: [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)

## <a name="run-the-diagnostic-tool"></a>Run the Diagnostic Tool
You can diagnose installation problems with the Access Panel Extension by downloading and running the Access Panel diagnostic tool:

1. [Click here to download the diagnostic tool.](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. Open the file, and press **Extract all** button.
   
    ![Press Extract All](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/extract1.png)
3. Then press the **Extract** button to continue.
   
    ![Press Extract](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/extract2.png)
4. To run the tool, right-click the file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.
   
    ![Open with > Microsoft Windows Based Script Host](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. You will then see the following diagnostic window, which describes what might be wrong with your installation.
   
    ![A sample of the diagnostic window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. Click "**YES**" to let the program fix the issues that have been found.
7. To save these changes, close every Internet Explorer window, and then open Internet Explorer again.<br />If you still can't access your apps, try the steps below.

## <a name="check-that-the-access-panel-extension-is-enabled"></a>Check that the Access Panel Extension is enabled
To verify that the Access Panel Extension is enabled in Internet Explorer:

1. In Internet Explorer, click the **Gear icon** on the top right corner of the window. Then select **Internet options**.<br />(In older versions of Internet Explorer you can find this under **Tools > Internet options**.
   
    ![Go to Tools > Internet Options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. Click the **Programs** tab, then click the **Manage add-ons** button.
   
    ![Click Manage Add-Ons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. In this dialog, select **Access Panel Extension** and then click the **Enable** button.
   
    ![Click Enable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. To save these changes, close every Internet Explorer window and then open Internet Explorer again.

## <a name="enable-extensions-for-inprivate-browsing"></a>Enable Extensions for InPrivate Browsing
If you are using the InPrivate Browsing mode:

1. In Internet Explorer, click the **Gear icon** on the top right corner of the window. Then select **Internet options**.<br />(In older versions of Internet Explorer you can find this under **Tools > Internet options**.
   
    ![A sample of the diagnostic window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. Go to the **Privacy** tab, then **uncheck** the checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</p>
   
    ![Uncheck Disable toolbars and extensions when InPrivate Browsing starts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. To save these changes, close every Internet Explorer window and then open Internet Explorer again.

## <a name="uninstall-the-access-panel-extension"></a>Uninstall the Access Panel Extension
To uninstall the Access Panel extension from your computer:

1. On your keyboard, press the **Windows key** to open the Start menu. When the menu is open, you can type anything to do a search. Type "Control Panel" and then open the **Control Panel** when it appears in the search results.
   
    ![Search for Control Panel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. In the top right corner of the Control Panel, change the **View by** option to **Large icons**. Then find and click the **Programs and Features** button.
   
    ![Chang the view to show Large Icons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. From the list, select **Access Panel Extension**, and the click the **Uninstall** button.
   
    ![Click Uninstall](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. You can then try to install the extension again to see if the problem has been resolved.

If you encounter issues uninstalling the extension, you can also remove it using the [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.

## <a name="related-articles"></a>Related Articles
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)
* [Application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)













