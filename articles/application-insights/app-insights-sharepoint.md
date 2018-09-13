---
title: Monitor a SharePoint site with Application Insights
description: Start monitoring a new application with a new instrumentation key
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: douge
ms.assetid: 2bfe5910-d673-4cf6-a5c1-4c115eae1be0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2016
ms.author: awills
ms.openlocfilehash: 79080ce6330ce1c287f046651b40f4e7ed094883
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550812"
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="95787-103">Monitor a SharePoint site with Application Insights</span><span class="sxs-lookup"><span data-stu-id="95787-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="95787-104">Azure Application Insights monitors the availability, performance and usage of your apps.</span><span class="sxs-lookup"><span data-stu-id="95787-104">Azure Application Insights monitors the availability, performance and usage of your apps.</span></span> <span data-ttu-id="95787-105">Here you'll learn how to set it up for a SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="95787-105">Here you'll learn how to set it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="95787-106">Create an Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="95787-106">Create an Application Insights resource</span></span>
<span data-ttu-id="95787-107">In the [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="95787-107">In the [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="95787-108">Choose ASP.NET as the application type.</span><span class="sxs-lookup"><span data-stu-id="95787-108">Choose ASP.NET as the application type.</span></span>

![Click Properties, select the key, and press ctrl+C](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="95787-110">The blade that opens is the place where you'll see performance and usage data about your app.</span><span class="sxs-lookup"><span data-stu-id="95787-110">The blade that opens is the place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="95787-111">To get back to it next time you login to Azure, you should find a tile for it on the start screen.</span><span class="sxs-lookup"><span data-stu-id="95787-111">To get back to it next time you login to Azure, you should find a tile for it on the start screen.</span></span> <span data-ttu-id="95787-112">Alternatively click Browse to find it.</span><span class="sxs-lookup"><span data-stu-id="95787-112">Alternatively click Browse to find it.</span></span>

## <a name="add-our-script-to-your-web-pages"></a><span data-ttu-id="95787-113">Add our script to your web pages</span><span class="sxs-lookup"><span data-stu-id="95787-113">Add our script to your web pages</span></span>
<span data-ttu-id="95787-114">In Quick Start, get the script for web pages:</span><span class="sxs-lookup"><span data-stu-id="95787-114">In Quick Start, get the script for web pages:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="95787-115">Insert the script just before the &lt;/head&gt; tag of every page you want to track. If your website has a master page, you can put the script there.</span><span class="sxs-lookup"><span data-stu-id="95787-115">Insert the script just before the &lt;/head&gt; tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="95787-116">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="95787-116">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="95787-117">The script contains the instrumentation key that directs the telemetry to your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="95787-117">The script contains the instrumentation key that directs the telemetry to your Application Insights resource.</span></span>

### <a name="add-the-code-to-your-site-pages"></a><span data-ttu-id="95787-118">Add the code to your site pages</span><span class="sxs-lookup"><span data-stu-id="95787-118">Add the code to your site pages</span></span>
#### <a name="on-the-master-page"></a><span data-ttu-id="95787-119">On the master page</span><span class="sxs-lookup"><span data-stu-id="95787-119">On the master page</span></span>
<span data-ttu-id="95787-120">If you can edit the site's master page, that will provide monitoring for every page in the site.</span><span class="sxs-lookup"><span data-stu-id="95787-120">If you can edit the site's master page, that will provide monitoring for every page in the site.</span></span>

<span data-ttu-id="95787-121">Check out the master page and edit it using SharePoint Designer or any other editor.</span><span class="sxs-lookup"><span data-stu-id="95787-121">Check out the master page and edit it using SharePoint Designer or any other editor.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="95787-122">Add the code just before the </head> tag.</span><span class="sxs-lookup"><span data-stu-id="95787-122">Add the code just before the </head> tag.</span></span> 

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="95787-123">Or on individual pages</span><span class="sxs-lookup"><span data-stu-id="95787-123">Or on individual pages</span></span>
<span data-ttu-id="95787-124">To monitor a limited set of pages, add the script separately to each page.</span><span class="sxs-lookup"><span data-stu-id="95787-124">To monitor a limited set of pages, add the script separately to each page.</span></span> 

<span data-ttu-id="95787-125">Insert a web part and embed the code snippet in it.</span><span class="sxs-lookup"><span data-stu-id="95787-125">Insert a web part and embed the code snippet in it.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="95787-126">View data about your app</span><span class="sxs-lookup"><span data-stu-id="95787-126">View data about your app</span></span>
<span data-ttu-id="95787-127">Redeploy your app.</span><span class="sxs-lookup"><span data-stu-id="95787-127">Redeploy your app.</span></span>

<span data-ttu-id="95787-128">Return to your application blade in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="95787-128">Return to your application blade in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="95787-129">The first events will appear in Search.</span><span class="sxs-lookup"><span data-stu-id="95787-129">The first events will appear in Search.</span></span> 

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="95787-130">Click Refresh after a few seconds if you're expecting more data.</span><span class="sxs-lookup"><span data-stu-id="95787-130">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="95787-131">From the overview blade, click **Usage analytics** to see to charts of users, sessions and page views:</span><span class="sxs-lookup"><span data-stu-id="95787-131">From the overview blade, click **Usage analytics** to see to charts of users, sessions and page views:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="95787-132">Click any chart to see more details - for example Page Views:</span><span class="sxs-lookup"><span data-stu-id="95787-132">Click any chart to see more details - for example Page Views:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="95787-133">Or Users:</span><span class="sxs-lookup"><span data-stu-id="95787-133">Or Users:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="95787-134">Capturing User Id</span><span class="sxs-lookup"><span data-stu-id="95787-134">Capturing User Id</span></span>
<span data-ttu-id="95787-135">The standard web page code snippet doesn't capture the user id from SharePoint, but you can do that with a small modification.</span><span class="sxs-lookup"><span data-stu-id="95787-135">The standard web page code snippet doesn't capture the user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="95787-136">Copy your app's instrumentation key from the Essentials drop-down in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="95787-136">Copy your app's instrumentation key from the Essentials drop-down in Application Insights.</span></span> 

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="95787-137">Substitute the instrumentation key for 'XXXX' in the snippet below.</span><span class="sxs-lookup"><span data-stu-id="95787-137">Substitute the instrumentation key for 'XXXX' in the snippet below.</span></span> 
2. <span data-ttu-id="95787-138">Embed the script in your SharePoint app instead of the snippet you get from the portal.</span><span class="sxs-lookup"><span data-stu-id="95787-138">Embed the script in your SharePoint app instead of the snippet you get from the portal.</span></span>

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get the current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for the target user. 
    // To get the PersonProperties object for the current user, use the 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load the PersonProperties object and send the request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if the executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if the executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a><span data-ttu-id="95787-139">Next Steps</span><span class="sxs-lookup"><span data-stu-id="95787-139">Next Steps</span></span>
* <span data-ttu-id="95787-140">[Web tests](app-insights-monitor-web-app-availability.md) to monitor the availability of your site.</span><span class="sxs-lookup"><span data-stu-id="95787-140">[Web tests](app-insights-monitor-web-app-availability.md) to monitor the availability of your site.</span></span>
* <span data-ttu-id="95787-141">[Application Insights](app-insights-overview.md) for other types of app.</span><span class="sxs-lookup"><span data-stu-id="95787-141">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->












