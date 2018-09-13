---
title: Monitoring usage and performance for Windows desktop apps
description: Analyze usage and performance of your Windows desktop app with HockeyApp and Application Insights.
services: application-insights
documentationcenter: windows
author: alancameronwills
manager: douge
ms.assetid: 19040746-3315-47e7-8c60-4b3000d2ddc4
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2016
ms.author: awills
ms.openlocfilehash: 35ca040ed123f6330f09f7fb1bc6be9ddaf61808
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670130"
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="06cb9-103">Monitoring usage and performance in Windows Desktop apps</span><span class="sxs-lookup"><span data-stu-id="06cb9-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="06cb9-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span><span class="sxs-lookup"><span data-stu-id="06cb9-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06cb9-105">We recommend [HockeyApp](https://hockeyapp.net) to distribute and monitor desktop and device apps.</span><span class="sxs-lookup"><span data-stu-id="06cb9-105">We recommend [HockeyApp](https://hockeyapp.net) to distribute and monitor desktop and device apps.</span></span> <span data-ttu-id="06cb9-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span><span class="sxs-lookup"><span data-stu-id="06cb9-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="06cb9-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span><span class="sxs-lookup"><span data-stu-id="06cb9-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="06cb9-108">Although telemetry can be sent to Application Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span><span class="sxs-lookup"><span data-stu-id="06cb9-108">Although telemetry can be sent to Application Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="to-send-telemetry-to-application-insights-from-a-windows-application"></a><span data-ttu-id="06cb9-109">To send telemetry to Application Insights from a Windows application</span><span class="sxs-lookup"><span data-stu-id="06cb9-109">To send telemetry to Application Insights from a Windows application</span></span>
1. <span data-ttu-id="06cb9-110">In the [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="06cb9-110">In the [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="06cb9-111">For application type, choose ASP.NET app.</span><span class="sxs-lookup"><span data-stu-id="06cb9-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="06cb9-112">Take a copy of the Instrumentation Key.</span><span class="sxs-lookup"><span data-stu-id="06cb9-112">Take a copy of the Instrumentation Key.</span></span> <span data-ttu-id="06cb9-113">Find the key in the Essentials drop-down of the new resource you just created.</span><span class="sxs-lookup"><span data-stu-id="06cb9-113">Find the key in the Essentials drop-down of the new resource you just created.</span></span> 
3. <span data-ttu-id="06cb9-114">In Visual Studio, edit the NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span><span class="sxs-lookup"><span data-stu-id="06cb9-114">In Visual Studio, edit the NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="06cb9-115">(Or choose Microsoft.ApplicationInsights if you just want the bare API, without the standard telemetry collection modules.)</span><span class="sxs-lookup"><span data-stu-id="06cb9-115">(Or choose Microsoft.ApplicationInsights if you just want the bare API, without the standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="06cb9-116">Set the instrumentation key either in your code:</span><span class="sxs-lookup"><span data-stu-id="06cb9-116">Set the instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="06cb9-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span><span class="sxs-lookup"><span data-stu-id="06cb9-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="06cb9-118">or in ApplicationInsights.config (if you installed one of the standard telemetry packages):</span><span class="sxs-lookup"><span data-stu-id="06cb9-118">or in ApplicationInsights.config (if you installed one of the standard telemetry packages):</span></span>
   
    <span data-ttu-id="06cb9-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="06cb9-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="06cb9-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span><span class="sxs-lookup"><span data-stu-id="06cb9-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span></span>
5. <span data-ttu-id="06cb9-121">[Use the API](app-insights-api-custom-events-metrics.md) to send telemetry.</span><span class="sxs-lookup"><span data-stu-id="06cb9-121">[Use the API](app-insights-api-custom-events-metrics.md) to send telemetry.</span></span>
6. <span data-ttu-id="06cb9-122">Run your app, and see the telemetry in the resource you created in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="06cb9-122">Run your app, and see the telemetry in the resource you created in the Azure Portal.</span></span>

## <a name="telemetry"></a><span data-ttu-id="06cb9-123">Example code</span><span class="sxs-lookup"><span data-stu-id="06cb9-123">Example code</span></span>
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative to setting ikey in config file:
            tc.InstrumentationKey = "key copied from portal";

            // Set session data:
            tc.Context.User.Id = Environment.UserName;
            tc.Context.Session.Id = Guid.NewGuid().ToString();
            tc.Context.Device.OperatingSystem = Environment.OSVersion.ToString();

            // Log a page view:
            tc.TrackPageView("Form1");
            ...
        }

        protected override void OnClosing(CancelEventArgs e)
        {
            stop = true;
            if (tc != null)
            {
                tc.Flush(); // only for desktop apps

                // Allow time for flushing:
                System.Threading.Thread.Sleep(1000);
            }
            base.OnClosing(e);
        }

```

## <a name="next-steps"></a><span data-ttu-id="06cb9-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="06cb9-124">Next steps</span></span>
* [<span data-ttu-id="06cb9-125">Create a dashboard</span><span class="sxs-lookup"><span data-stu-id="06cb9-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="06cb9-126">Diagnostic Search</span><span class="sxs-lookup"><span data-stu-id="06cb9-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="06cb9-127">Explore metrics</span><span class="sxs-lookup"><span data-stu-id="06cb9-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="06cb9-128">Write Analytics queries</span><span class="sxs-lookup"><span data-stu-id="06cb9-128">Write Analytics queries</span></span>](app-insights-analytics.md)

