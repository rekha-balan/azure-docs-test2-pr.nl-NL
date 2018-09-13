---
title: Microsoft Dynamics CRM and Azure Application Insights | Microsoft Docs
description: Get telemetry from Microsoft Dynamics CRM Online using Application Insights. Walkthrough of setup, getting data, visualization and export.
services: application-insights
documentationcenter: ''
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: awills
ms.openlocfilehash: 451a32e2ca18f0b175369a15d9b4f228ede6d013
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550919"
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a>Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights
This article shows you how to get telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/). We’ll walk through the complete process of adding Application Insights script to your application, capturing data, and data visualization.

> [!NOTE]
> [Browse the sample solution](https://dynamicsandappinsights.codeplex.com/).
> 
> 

## <a name="add-application-insights-to-new-or-existing-crm-online-instance"></a>Add Application Insights to new or existing CRM Online instance
To monitor your application, you add an Application Insights SDK to your application. The SDK sends telemetry to the [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export the data to storage.

### <a name="create-an-application-insights-resource-in-azure"></a>Create an Application Insights resource in Azure
1. Get [an account in Microsoft Azure](http://azure.com/pricing). 
2. Sign into the [Azure portal](https://portal.azure.com) and add a new Application Insights resource. This is where your data will be processed and displayed.
   
    ![Click +, Developer Services, Application Insights.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/01.png)
   
    Choose ASP.NET as the application type.
3. Open the Getting Started page and open "Monitor and diagnose client side".
   
    ![Code snippet for insertion in your web page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/03.png)

**Keep the code page open** while you do the next step in another browser window. You'll need the code soon. 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a>Create a JavaScript web resource in Microsoft Dynamics CRM
1. Open your CRM Online instance and login with administrator privileges.
2. Open Microsoft Dynamics CRM Settings, Customizations, Customize the System
   
    ![Microsoft Dynamics CRM settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/04.png)
   
    ![Settings > Customizations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/05.png)

    ![Customize the system option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/06.png)

1. Create a JavaScript resource.
   
    ![New Web Resource dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/07.png)
   
    Give it a name, select **Script (JScript)** and open the text editor.
   
    ![Open the text editor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/08.png)
2. Copy the code from Application Insights. While copying make sure to ignore script tags. Refer below screenshot:
   
    ![Set your instrumentation key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/09.png)
   
    The code includes the instrumentation key that identifies your Application insights resource.
3. Save and publish.
   
    ![Save and publish](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a>Instrument Forms
1. In Microsoft CRM Online, open the Account form
   
    ![Account form](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/11.png)
2. Open the form Properties
   
    ![Form properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/12.png)
3. Add the JavaScript web resource that you created
   
    ![Add menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/13.png)
   
    ![Add the web resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/14.png)
4. Save and publish your form customizations.

## <a name="metrics-captured"></a>Metrics captured
You have now set up telemetry capture for the form. Whenever it is used, data will be sent to your Application Insights resource.

Here are samples of the data that you'll see.

#### <a name="application-health"></a>Application health
![Example page load time](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/15.png)

![Example page views chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/16.png)

Browser exceptions:

![Browser exceptions chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/17.png)

Click the chart to get more detail:

![Exceptions list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a>Usage
![Users, sessions and page views](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/19.png)

![Sesion charts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/20.png)

![Browser versions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a>Browsers
![Breakdown of page load time](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/22.png)

![Count of sessions by browser version](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a>Geolocation
![Session count by country](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/24.png)

![Sessions and users by country](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a>Inside page view request
![Page view summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/26.png)

![Search on page view events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/27.png)

![Similar page views](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/28.png)

![Page view properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/29.png)

![Pages per session](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a>Sample code
[Browse the sample code](https://dynamicsandappinsights.codeplex.com/).

## <a name="power-bi"></a>Power BI
You can do even deeper analysis if you [export the data to Microsoft Power BI](app-insights-export-power-bi.md).

## <a name="sample-microsoft-dynamics-crm-solution"></a>Sample Microsoft Dynamics CRM Solution
[Here is the sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).

## <a name="learn-more"></a>Learn more
* [What is Application Insights?](app-insights-overview.md)
* [Application Insights for web pages](app-insights-javascript.md)
* [More samples and walkthroughs](app-insights-code-samples.md)





























