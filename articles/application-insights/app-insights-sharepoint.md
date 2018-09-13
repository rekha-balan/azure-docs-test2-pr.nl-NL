---
title: Monitor a SharePoint site with Application Insights
description: Start monitoring a new application with a new instrumentation key
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.assetid: 2bfe5910-d673-4cf6-a5c1-4c115eae1be0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: mbullwin
ms.openlocfilehash: 3a7d657a21b414d51375f912513ae045adec6d6e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818563"
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="d4dca-103">Monitor a SharePoint site with Application Insights</span><span class="sxs-lookup"><span data-stu-id="d4dca-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="d4dca-104">Azure Application Insights monitors the availability, performance and usage of your apps.</span><span class="sxs-lookup"><span data-stu-id="d4dca-104">Azure Application Insights monitors the availability, performance and usage of your apps.</span></span> <span data-ttu-id="d4dca-105">Here you'll learn how to set it up for a SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="d4dca-105">Here you'll learn how to set it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="d4dca-106">Create an Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="d4dca-106">Create an Application Insights resource</span></span>
<span data-ttu-id="d4dca-107">In the [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="d4dca-107">In the [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="d4dca-108">Choose ASP.NET as the application type.</span><span class="sxs-lookup"><span data-stu-id="d4dca-108">Choose ASP.NET as the application type.</span></span>

![Click Properties, select the key, and press ctrl+C](./media/app-insights-sharepoint/001.png)

<span data-ttu-id="d4dca-110">The window that opens is the place where you'll see performance and usage data about your app.</span><span class="sxs-lookup"><span data-stu-id="d4dca-110">The window that opens is the place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="d4dca-111">To get back to it next time you login to Azure, you should find a tile for it on the start screen.</span><span class="sxs-lookup"><span data-stu-id="d4dca-111">To get back to it next time you login to Azure, you should find a tile for it on the start screen.</span></span> <span data-ttu-id="d4dca-112">Alternatively click Browse to find it.</span><span class="sxs-lookup"><span data-stu-id="d4dca-112">Alternatively click Browse to find it.</span></span>

## <a name="add-the-script-to-your-web-pages"></a><span data-ttu-id="d4dca-113">Add the script to your web pages</span><span class="sxs-lookup"><span data-stu-id="d4dca-113">Add the script to your web pages</span></span>

```HTML
<!-- 
To collect user behavior analytics tools about your application, 
insert the following script into each page you want to track.
Place this code immediately before the closing </head> tag,
and before any other scripts. Your first data will appear 
automatically in just a few seconds.
-->
<script type="text/javascript">
var appInsights=window.appInsights||function(a){
  function b(a){c[a]=function(){var b=arguments;c.queue.push(function(){c[a].apply(c,b)})}}var c={config:a},d=document,e=window;setTimeout(function(){var b=d.createElement("script");b.src=a.url||"https://az416426.vo.msecnd.net/scripts/a/ai.0.js",d.getElementsByTagName("script")[0].parentNode.appendChild(b)});try{c.cookie=d.cookie}catch(a){}c.queue=[];for(var f=["Event","Exception","Metric","PageView","Trace","Dependency"];f.length;)b("track"+f.pop());if(b("setAuthenticatedUserContext"),b("clearAuthenticatedUserContext"),b("startTrackEvent"),b("stopTrackEvent"),b("startTrackPage"),b("stopTrackPage"),b("flush"),!a.disableExceptionTracking){f="onerror",b("_"+f);var g=e[f];e[f]=function(a,b,d,e,h){var i=g&&g(a,b,d,e,h);return!0!==i&&c["_"+f](a,b,d,e,h),i}}return c
  }({
      instrumentationKey:"<your instrumentation key>"
  });
  
window.appInsights=appInsights,appInsights.queue&&0===appInsights.queue.length&&appInsights.trackPageView();
</script>
```

<span data-ttu-id="d4dca-114">Insert the script just before the &lt;/head&gt; tag of every page you want to track. If your website has a master page, you can put the script there.</span><span class="sxs-lookup"><span data-stu-id="d4dca-114">Insert the script just before the &lt;/head&gt; tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="d4dca-115">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="d4dca-115">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="d4dca-116">The script contains the instrumentation key that directs the telemetry to your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="d4dca-116">The script contains the instrumentation key that directs the telemetry to your Application Insights resource.</span></span>

### <a name="add-the-code-to-your-site-pages"></a><span data-ttu-id="d4dca-117">Add the code to your site pages</span><span class="sxs-lookup"><span data-stu-id="d4dca-117">Add the code to your site pages</span></span>
#### <a name="on-the-master-page"></a><span data-ttu-id="d4dca-118">On the master page</span><span class="sxs-lookup"><span data-stu-id="d4dca-118">On the master page</span></span>
<span data-ttu-id="d4dca-119">If you can edit the site's master page, that will provide monitoring for every page in the site.</span><span class="sxs-lookup"><span data-stu-id="d4dca-119">If you can edit the site's master page, that will provide monitoring for every page in the site.</span></span>

<span data-ttu-id="d4dca-120">Check out the master page and edit it using SharePoint Designer or any other editor.</span><span class="sxs-lookup"><span data-stu-id="d4dca-120">Check out the master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="d4dca-121">Add the code just before the </head> tag.</span><span class="sxs-lookup"><span data-stu-id="d4dca-121">Add the code just before the </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="d4dca-122">Or on individual pages</span><span class="sxs-lookup"><span data-stu-id="d4dca-122">Or on individual pages</span></span>
<span data-ttu-id="d4dca-123">To monitor a limited set of pages, add the script separately to each page.</span><span class="sxs-lookup"><span data-stu-id="d4dca-123">To monitor a limited set of pages, add the script separately to each page.</span></span> 

<span data-ttu-id="d4dca-124">Insert a web part and embed the code snippet in it.</span><span class="sxs-lookup"><span data-stu-id="d4dca-124">Insert a web part and embed the code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="d4dca-125">View data about your app</span><span class="sxs-lookup"><span data-stu-id="d4dca-125">View data about your app</span></span>
<span data-ttu-id="d4dca-126">Redeploy your app.</span><span class="sxs-lookup"><span data-stu-id="d4dca-126">Redeploy your app.</span></span>

<span data-ttu-id="d4dca-127">Return to your application blade in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d4dca-127">Return to your application blade in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="d4dca-128">The first events will appear in Search.</span><span class="sxs-lookup"><span data-stu-id="d4dca-128">The first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="d4dca-129">Click Refresh after a few seconds if you're expecting more data.</span><span class="sxs-lookup"><span data-stu-id="d4dca-129">Click Refresh after a few seconds if you're expecting more data.</span></span>

## <a name="capturing-user-id"></a><span data-ttu-id="d4dca-130">Capturing User Id</span><span class="sxs-lookup"><span data-stu-id="d4dca-130">Capturing User Id</span></span>
<span data-ttu-id="d4dca-131">The standard web page code snippet doesn't capture the user id from SharePoint, but you can do that with a small modification.</span><span class="sxs-lookup"><span data-stu-id="d4dca-131">The standard web page code snippet doesn't capture the user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="d4dca-132">Copy your app's instrumentation key from the Essentials drop-down in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d4dca-132">Copy your app's instrumentation key from the Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="d4dca-133">Substitute the instrumentation key for 'XXXX' in the snippet below.</span><span class="sxs-lookup"><span data-stu-id="d4dca-133">Substitute the instrumentation key for 'XXXX' in the snippet below.</span></span> 
2. <span data-ttu-id="d4dca-134">Embed the script in your SharePoint app instead of the snippet you get from the portal.</span><span class="sxs-lookup"><span data-stu-id="d4dca-134">Embed the script in your SharePoint app instead of the snippet you get from the portal.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="d4dca-135">Next Steps</span><span class="sxs-lookup"><span data-stu-id="d4dca-135">Next Steps</span></span>
* <span data-ttu-id="d4dca-136">[Web tests](app-insights-monitor-web-app-availability.md) to monitor the availability of your site.</span><span class="sxs-lookup"><span data-stu-id="d4dca-136">[Web tests](app-insights-monitor-web-app-availability.md) to monitor the availability of your site.</span></span>
* <span data-ttu-id="d4dca-137">[Application Insights](app-insights-overview.md) for other types of app.</span><span class="sxs-lookup"><span data-stu-id="d4dca-137">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


