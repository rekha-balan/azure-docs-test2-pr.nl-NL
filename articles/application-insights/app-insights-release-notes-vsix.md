---
title: Release notes for Visual Studio Extension for Developer Analytics
description: The latest updates for Visual Studio tools for Developer Analytics.
services: application-insights
documentationcenter: ''
author: acearun
manager: carmonm
ms.assetid: 2001db30-efc5-417a-a413-93c1b218975f
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: aruna
ms.openlocfilehash: af4ab03fd31bcfd035dfacc1ee156daf9d251dfd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556178"
---
# <a name="release-notes-for-developer-analytics-tools"></a>Release Notes for Developer Analytics Tools

## <a name="version-718-visual-studio-2015"></a>Version 7.18 (Visual Studio 2015)

* Redesigned toast notifications.
* "Not" filters in the Detail view for events in Application Insights Search.
* Bug fixes

## <a name="version-86-visual-studio-2017-rtw-and-rc4-and-version-717-visual-studio-2015"></a>Version 8.6 (Visual Studio 2017 RTW and RC4) and Version 7.17 (Visual Studio 2015)

* Annotations marking when you publish your app from Visual Studio are now made to your data in the Metrics Explorer in the Azure Portal
* Markers are now added to scrollbars in code files, corresponding to red and yellow CodeLens warnings from Application Insights
* Updated pricing information in the Configuration window
* Bug fixes

[See the detailed notes here](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#devanalytics)

## <a name="version-716-visual-studio-2015"></a>Version 7.16 (Visual Studio 2015)

* Bug fixes

## <a name="version-85-visual-studio-2017-rc3-and-version-715-visual-studio-2015"></a>Version 8.5 (Visual Studio 2017 RC3) and Version 7.15 (Visual Studio 2015)

* CodeLens now shows both debug and live telemetry data in projects that send data to an Application Insights resource
* Application Insights pricing information is now shown in the Configuration window
* CodeLens for requests and exceptions now supports ASP.NET projects written in Visual Basic
* Application Insights Search now shows un-sampled event counts for events that have been sampled
* Bug fixes

## <a name="version-714-visual-studio-2015"></a>Version 7.14 (Visual Studio 2015)

* Search support for availability (web test) and page view events
* Trends support for availability (web test) and page view events
* Diagnostic Tools and event details label for SDK Adaptive Sampling
* Bug fixes

## <a name="version-712-visual-studio-2015"></a>Version 7.12 (Visual Studio 2015)

* New publish notification format
* Bug fixes

## <a name="version-84-visual-studio-2017-rc2-and-version-711-visual-studio-2015"></a>Version 8.4 (Visual Studio 2017 RC2) and Version 7.11 (Visual Studio 2015)

* CodeLens shows requests for local debug sessions for projects with the Application Insights SDK
* CodeLens can take you directly to Application Analytics to see user impact
* Insert JavaScript to collect page views
* Bug fixes

## <a name="version-710-visual-studio-2015"></a>Version 7.10 (Visual Studio 2015)

* New design for the Application Insights Configuration window
* Bug fixes

## <a name="version-79-visual-studio-2015"></a>Version 7.9 (Visual Studio 2015)

* CodeLens shows exceptions that have occurred during local debug sessions for projects with the Application Insights SDK
* Bug fixes

## <a name="version-83-visual-studio-2017-rc-and-version-78-visual-studio-2015"></a>Version 8.3 (Visual Studio 2017 RC) and Version 7.8 (Visual Studio 2015)

* New experience for adding Application Insights in the Configuration window
* Bug fixes

## <a name="version-77-visual-studio-2015"></a>Version 7.7 (Visual Studio 2015)

* More accurate mappings from telemetry events to methods using custom ASP.NET routing
* Bug fixes

## <a name="version-76-visual-studio-2015"></a>Version 7.6 (Visual Studio 2015)

* Analyze events involved in an operation from the new Track Operation tab on events in the Search tool
* Bug fixes

## <a name="version-75-visual-studio-2015"></a>Version 7.5 (Visual Studio 2015)

* Production telemetry information for requests in Diagnostic Tools
* Work Item creation from Related Items in the Search tool
* Bug fixes

## <a name="version-74-visual-studio-2015"></a>Version 7.4 (Visual Studio 2015)

* The filter pane in Trends is now resizable
* Bug fixes

## <a name="version-73-visual-studio-2015"></a>Version 7.3 (Visual Studio 2015)

* Requests in CodeLens
* Configuration window
* HockeyApp SDK updated to v4.2.2
* Bug fixes

## <a name="version-72-visual-studio-2015"></a>Version 7.2 (Visual Studio 2015)

* Bug fixes

## <a name="version-71-visual-studio-2015"></a>Version 7.1 (Visual Studio 2015)

* Telemetry Readiness indicator in Application Insights Trends
* Bug fixes

## <a name="version-70"></a>Version 7.0
### <a name="azure-application-insights-trends"></a>Azure Application Insights Trends
Azure Application Insights is a new tool in Visual Studio that you can use to help you analyze how your app operates over time. To get started, on the **Application Insights** toolbar button or in the Application Insights Search window, choose **Explore Telemetry Trends**. Or, on the **View** menu, click **Other Windows**, and then click **Application Insights Trends**. Choose one of five common queries to get started. You can analyze different data sets based on telemetry types, time ranges, and other properties. To find anomalies in your data, choose one of the anomaly options in the **View Type** drop-down list. The filtering options at the bottom of the window make it easy to hone in on specific subsets of your telemetry.

![Application Insights Trends](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/Trends.png)

### <a name="exceptions-in-codelens"></a>Exceptions in CodeLens
Exception telemetry is now displayed in CodeLens. If you've connected your project to the Application Insights service, you'll see the number of exceptions that have occurred in each method in production in the past 24 hours. From CodeLens, you can jump to Search or Trends to investigate the exceptions in more detail.

![Exceptions in CodeLens](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/ExceptionsCodeLens.png)

### <a name="aspnet-core-support"></a>ASP.NET Core support
Application Insights now supports ASP.NET Core RC2 projects in Visual Studio. You can add Application Insights to new ASP.NET Core RC2 projects from the **New Project** dialog, as in the following screenshot. Or, you can add it to an existing project, right-click the project in Solution Explorer, and then click **Add Application Insights Telemetry**.

![ASP.NET Core support](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/NetCoreSupport.png)

ASP.NET 5 RC1 and ASP.NET Core RC2 projects also have new support in the Diagnostic Tools window. You'll see Application Insights events like requests and exceptions from your ASP.NET app while you debug locally on your PC. From each event, click **Search** to drill down for more information.

![Diagnostic Tools support](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/DiagnosticTools.png)

### <a name="hockeyapp-for-universal-windows-apps"></a>HockeyApp for Universal Windows apps
In addition to beta distribution and user feedback, HockeyApp provides symbolicated crash reporting for your Universal Windows apps. We've made it even easier to add the HockeyApp SDK: right-click on your Universal Windows project, and then click **Hockey App - Enable Crash Analytics**. This installs the SDK, sets up crash collection, and provisions a HockeyApp resource in the cloud, all without uploading your app to the HockeyApp service.

Other new features:

* We've made the Application Insights Search experience faster and more intuitive. Now, time ranges and detail filters are automatically applied as you select them.
* Also in Application Insights Search, now there's an option to jump to the code directly from the request telemetry.
* We've made improvements to the HockeyApp sign-in experience.
* In Diagnostic Tools, production telemetry information for exceptions is displayed.

## <a name="version-52"></a>Version 5.2
We are happy to announce the introduction of HockeyApp scenarios in Visual Studio. The first integration is in beta distribution of Universal Windows apps and Windows Forms apps from within Visual Studio.

With beta distribution, you upload early versions of your apps to HockeyApp for distribution to a selected subset of customers or testers. Beta distribution, combined with HockeyApp crash collection and user feedback features, can provide you with valuable information about your app before you make a broad release. You can use this information to address issues with your app so that you can avoid or minimize future problems, such as low app ratings, negative feedback, and so on.

Check out how simple it is to upload builds for beta distribution from within Visual Studio.

### <a name="universal-windows-apps"></a>Universal Windows apps
The context menu for a Universal Windows app project node now includes an option to upload your build to HockeyApp.

![Project context menu for Universal Windows apps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/UniversalContextMenu.png)

Choose the item and the HockeyApp upload dialog box opens. You will need a HockeyApp account to upload your build. If you are a new user, don't worry. Creating an account is a simple process.

When you are connected, you will see the upload form in the dialog.

![Upload dialog for Universal Windows apps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/UniversalUploadDialog.png)

Select the content to upload (an .appxbundle or .appx file), and then choose release options in the wizard. Optionally, you can add release notes on the next page. Choose **Finish** to begin the upload.

When the upload is complete, a HockeyApp notification with confirmation and a link to the app in the HockeyApp portal appears.

![Upload complete notification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/UploadComplete.png)

That’s it! You've just uploaded a build for beta distribution with just a few clicks.

You can manage your application in numerous ways in the HockeyApp portal. This includes inviting users, viewing crash reports and feedback, changing details, and so on.

![HockeyApp portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/HockeyAppPortal.png)

See the [HockeyApp Knowledge Base](http://support.hockeyapp.net/kb/app-management-2) for more details about app management.

### <a name="windows-forms-apps"></a>Windows Forms apps
The context menu for a Windows Form project node now includes an option to upload your build to HockeyApp.

![Project context menu for Windows Forms apps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/WinFormContextMenu.png)

This opens the HockeyApp upload dialog, which is similar to the one in a Universal Windows app.

![Upload dialog for Windows Forms apps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/WinFormsUploadDialog.png)

Note a new field in this wizard, for specifying the version of the app. For Universal Windows apps, the information is populated from the manifest. Windows Forms apps, unfortunately, don’t have an equivalent to this feature. You will need to specify them manually.

The rest of the flow is similar to Universal Windows apps: choose build and release options, add release notes, upload, and manage in the HockeyApp portal.

It’s as simple as that. Give it a try and let us know what you think.

## <a name="version-43"></a>Version 4.3
### <a name="search-telemetry-from-local-debug-sessions"></a>Search telemetry from local debug sessions
With this release, you can now search for Application Insights telemetry generated in the Visual Studio debug session. Before, you could use search only if you registered your app with Application Insights. Now, your app only needs to have the Application Insights SDK installed to search for local telemetry.

If you have an ASP.NET application with the Application Insights SDK, do the following steps to use Search.

1. Debug your application.
2. Open Application Insights Search in one of these ways:
   * On the **View** menu, click **Other Windows**, and then click **Application Insights Search**.
   * Click the **Application Insights** toolbar button.
   * In Solution Explorer, expand **ApplicationInsights.config**, and then click **Search debug session telemetry**.
3. If you haven't signed up with Application Insights, the Search window will open in debug session telemetry mode.
4. Click the **Search** icon to see your local telemetry.

![Upload complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/LocalSearch.png)

## <a name="version-42"></a>Version 4.2
In this release, we added features to make searching for data easier in the context of events, with the ability to jump to code from more data events, and an effortless experience to send your logging data to Application Insights. This extension is updated monthly. If you have feedback or feature requests, send it to aidevtools@microsoft.com.

### <a name="no-click-logging-experience"></a>No-click logging experience
If you're already using NLog, log4net, or System.Diagnostics.Tracing, you don't have to worry about moving all of your traces to Application Insights. In this release, we've integrated the Application Insights logging adapters with the normal configuration experience.
If you already have one of these logging frameworks configured, the following section describes how to get it.
**If you've already added Application Insights:**

1. Right-click the project node, and then click **Application Insights**, and then click **Configure Application Insights**. Make sure that you see the option to add the correct adapter in the configuration window.
2. Alternatively, when you build the solution, note the pop-up window that appears on the top right of your screen and click **Configure**.

![Logging notification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/LoggingToast.png)

When you have the Logging adapter installed, run your application and make sure you see the data in the diagnostic tools tab, like this:

![Traces](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/Traces.png)

### <a name="jump-to-or-find-the-code-where-the-telemetry-event-property-is-emitted"></a>Jump to or find the code where the telemetry event property is emitted
With the new release user can click on any value in the event detail and this will search for a matching string in the current open solution. Results will show up in Visual Studio "Find Results" list as shown below:

![Find match](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/FindMatch.png)

### <a name="new-search-window-for-when-you-are-not-signed-in"></a>New Search window for when you are not signed in
We've improved the look of the Application Insights Search window to help you search your data while your app is in production.

![Search window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/SearchWindow.png)

### <a name="see-all-telemetry-events-associated-with-the-event"></a>See all telemetry events associated with the event
We've added a new tab, with predefined queries for all data related to the telemetry event the user is viewing, next to the tab for event details. For example, a request has a field called **Operation ID**. Every event associated to this request has the same value for **Operation ID**. If an exception occurs while the operation is processing the request, the exception is given the same operation ID as the request to make it easier to find. If you're looking at a request, click **All telemetry for this operation** to open a new tab that displays the new search results.

![Related items](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/RelatedItems.png)

### <a name="forward-and-back-history-in-search"></a>Forward and Back history in Search
Now you can go back and forth between search results.

![Go back](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/GoBAck.png)

## <a name="version-41"></a>Version 4.1
This release comes with a number of new features and updates. You need to have Update 1 installed to install this release.

### <a name="jump-from-an-exception-to-method-in-source-code"></a>Jump from an exception to method in source code
Now, if you view exceptions from your production app in the Application Insights Search window, you can jump to the method in your code where the exception is occurring. You only need to have the correct project loaded and Application Insights takes care of the rest! (To learn more about the Application Insights Search window, see the release notes for Version 4.0 in the following sections.)

How does it work? You can use Applications Insights Search even when a solution isn't open. The stack trace area displays an information message, and many of the items in the stack trace are unavailable.

If file information is available, some items might be links, but the solution information item will still be visible.

If you click the hyperlink, you'll jump to the location of the selected method in your code. There might be a difference in the version number, but the feature, to jump to the correct version of the code, will come in later releases.

![Click exception details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/jumptocode.png)

### <a name="new-entry-points-to-the-search-experience-in-solution-explorer"></a>New entry points to the Search experience in Solution Explorer
Now you can access Search through Solution Explorer.

![Search in Solution Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/searchentry.png)

### <a name="displays-a-notification-when-publish-is-completed"></a>Displays a notification when publish is completed
A pop-up dialog box appears when the project is published online, so that you can view your Application Insights data in production.

![Publish complete notification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/publishtoast.png)

## <a name="version-40"></a>Version 4.0
### <a name="search-application-insights-data-from-within-visual-studio"></a>Search Application Insights data from within Visual Studio
Like the search function in the Application Insights portal, now in Visual Studio you can filter and search on event types, property values, and text, and then inspect individual events.

![Search window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/search.png)

### <a name="see-data-coming-from-your-local-computer-in-diagnostic-tools"></a>See data coming from your local computer in Diagnostic Tools
You can view your telemetry, in addition to other debugging data, on the Visual Studio Diagnostic Tools page. Only ASP.NET 4.5 is supported.

![Diagnostic Tools page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/diagtools.png)

### <a name="add-the-sdk-to-your-project-without-signing-in-to-azure"></a>Add the SDK to your project without signing in to Azure
You no longer have to sign in to Azure to add Application Insights packages to your project, either through the **New Project** dialog or from the project context menu. If you do sign in, the SDK will be installed and configured to send telemetry to the portal as before. If you don’t sign in, the SDK will be added to your project and it will generate telemetry for the diagnostic hub. You can configure it later if you want.

![New Project dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-release-notes-vsix/newproject.png)

### <a name="device-support"></a>Device support
At *Connect();* 2015, we [announced](https://azure.microsoft.com/blog/deep-diagnostics-for-web-apps-with-application-insights/) that our mobile developer experience for devices is HockeyApp. HockeyApp helps you distribute beta builds to your testers, collect and analyze all crashes from your app, and collect feedback directly from your customers.
HockeyApp supports your app on whichever platform you choose to build it, whether that be iOS, Android, or Windows, or a cross-platform solution like Xamarin, Cordova, or Unity.

In future releases of the Application Insights extension, we’ll introduce a more integrated experience between HockeyApp and Visual Studio. For now, you can start with HockeyApp by simply adding the NuGet reference. See the [documentation](http://support.hockeyapp.net/kb/client-integration-windows-and-windows-phone) for more information.























