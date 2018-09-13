---
title: Troubleshooting degraded status on Azure Traffic Manager
description: How to troubleshoot Traffic Manager profiles when it shows as degraded status.
services: traffic-manager
documentationcenter: ''
author: kumudd
manager: timlt
ms.assetid: 8af0433d-e61b-4761-adcc-7bc9b8142fc6
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: eb287afd8768f93db574abc3113f429f26ef33aa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540910"
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="1f19c-103">Troubleshooting degraded state on Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="1f19c-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="1f19c-104">This article describes how to troubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span><span class="sxs-lookup"><span data-stu-id="1f19c-104">This article describes how to troubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="1f19c-105">For this scenario, consider that you have configured a Traffic Manager profile pointing to some of your cloudapp.net hosted services.</span><span class="sxs-lookup"><span data-stu-id="1f19c-105">For this scenario, consider that you have configured a Traffic Manager profile pointing to some of your cloudapp.net hosted services.</span></span> <span data-ttu-id="1f19c-106">When you check the health of your traffic manager, you see that the Status is Degraded.</span><span class="sxs-lookup"><span data-stu-id="1f19c-106">When you check the health of your traffic manager, you see that the Status is Degraded.</span></span>

![degraded state](https://docstestmedia1.blob.core.windows.net/azure-media/articles/traffic-manager/media/traffic-manager-troubleshooting-degraded/traffic-manager-degraded.png)

<span data-ttu-id="1f19c-108">If you go into the Endpoints tab of that profile, you see one or more of the endpoints with an Offline status:</span><span class="sxs-lookup"><span data-stu-id="1f19c-108">If you go into the Endpoints tab of that profile, you see one or more of the endpoints with an Offline status:</span></span>

![offline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/traffic-manager/media/traffic-manager-troubleshooting-degraded/traffic-manager-offline.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="1f19c-110">Understanding Traffic Manager probes</span><span class="sxs-lookup"><span data-stu-id="1f19c-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="1f19c-111">Traffic Manager considers an endpoint to be ONLINE only when the probe receives an HTTP 200 response back from the probe path.</span><span class="sxs-lookup"><span data-stu-id="1f19c-111">Traffic Manager considers an endpoint to be ONLINE only when the probe receives an HTTP 200 response back from the probe path.</span></span> <span data-ttu-id="1f19c-112">Any other non-200 response is a failure.</span><span class="sxs-lookup"><span data-stu-id="1f19c-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="1f19c-113">A 30x redirect fails, even if the redirected URL returns a 200.</span><span class="sxs-lookup"><span data-stu-id="1f19c-113">A 30x redirect fails, even if the redirected URL returns a 200.</span></span>
* <span data-ttu-id="1f19c-114">For HTTPs probes, certificate errors are ignored.</span><span class="sxs-lookup"><span data-stu-id="1f19c-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="1f19c-115">The actual content of the probe path doesn't matter, as long as a 200 is returned.</span><span class="sxs-lookup"><span data-stu-id="1f19c-115">The actual content of the probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="1f19c-116">Probing a URL to some static content like "/favicon.ico" is a common technique.</span><span class="sxs-lookup"><span data-stu-id="1f19c-116">Probing a URL to some static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="1f19c-117">Dynamic content, like the ASP pages, may not always return 200, even when the application is healthy.</span><span class="sxs-lookup"><span data-stu-id="1f19c-117">Dynamic content, like the ASP pages, may not always return 200, even when the application is healthy.</span></span>
* <span data-ttu-id="1f19c-118">A best practice is to set the Probe path to something that has enough logic to determine that the site is up or down.</span><span class="sxs-lookup"><span data-stu-id="1f19c-118">A best practice is to set the Probe path to something that has enough logic to determine that the site is up or down.</span></span> <span data-ttu-id="1f19c-119">In the previous example, by setting the path to "/favicon.ico", you are only testing that w3wp.exe is responding.</span><span class="sxs-lookup"><span data-stu-id="1f19c-119">In the previous example, by setting the path to "/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="1f19c-120">This probe may not indicate that your web application is healthy.</span><span class="sxs-lookup"><span data-stu-id="1f19c-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="1f19c-121">A better option would be to set a path to a something such as "/Probe.aspx" that has logic to determine the health of the site.</span><span class="sxs-lookup"><span data-stu-id="1f19c-121">A better option would be to set a path to a something such as "/Probe.aspx" that has logic to determine the health of the site.</span></span> <span data-ttu-id="1f19c-122">For example, you could use performance counters to CPU utilization or measure the number of failed requests.</span><span class="sxs-lookup"><span data-stu-id="1f19c-122">For example, you could use performance counters to CPU utilization or measure the number of failed requests.</span></span> <span data-ttu-id="1f19c-123">Or you could attempt to access database resources or session state to make sure that the web application is working.</span><span class="sxs-lookup"><span data-stu-id="1f19c-123">Or you could attempt to access database resources or session state to make sure that the web application is working.</span></span>
* <span data-ttu-id="1f19c-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic to all endpoints.</span><span class="sxs-lookup"><span data-stu-id="1f19c-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic to all endpoints.</span></span> <span data-ttu-id="1f19c-125">This behavior ensures that problems with the probing mechanism do not result in a complete outage of your service.</span><span class="sxs-lookup"><span data-stu-id="1f19c-125">This behavior ensures that problems with the probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1f19c-126">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="1f19c-126">Troubleshooting</span></span>

<span data-ttu-id="1f19c-127">To troubleshoot a probe failure, you need a tool that shows the HTTP status code return from the probe URL.</span><span class="sxs-lookup"><span data-stu-id="1f19c-127">To troubleshoot a probe failure, you need a tool that shows the HTTP status code return from the probe URL.</span></span> <span data-ttu-id="1f19c-128">There are many tools available that show you the raw HTTP response.</span><span class="sxs-lookup"><span data-stu-id="1f19c-128">There are many tools available that show you the raw HTTP response.</span></span>

* [<span data-ttu-id="1f19c-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="1f19c-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="1f19c-130">curl</span><span class="sxs-lookup"><span data-stu-id="1f19c-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="1f19c-131">wget</span><span class="sxs-lookup"><span data-stu-id="1f19c-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="1f19c-132">Also, you can use the Network tab of the F12 Debugging Tools in Internet Explorer to view the HTTP responses.</span><span class="sxs-lookup"><span data-stu-id="1f19c-132">Also, you can use the Network tab of the F12 Debugging Tools in Internet Explorer to view the HTTP responses.</span></span>

<span data-ttu-id="1f19c-133">For this example we want to see the response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span><span class="sxs-lookup"><span data-stu-id="1f19c-133">For this example we want to see the response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="1f19c-134">The following PowerShell example illustrates the problem.</span><span class="sxs-lookup"><span data-stu-id="1f19c-134">The following PowerShell example illustrates the problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="1f19c-135">Example output:</span><span class="sxs-lookup"><span data-stu-id="1f19c-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="1f19c-136">Notice that we received a redirect response.</span><span class="sxs-lookup"><span data-stu-id="1f19c-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="1f19c-137">As stated previously, any StatusCode other than 200 is considered a failure.</span><span class="sxs-lookup"><span data-stu-id="1f19c-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="1f19c-138">Traffic Manager changes the endpoint status to Offline.</span><span class="sxs-lookup"><span data-stu-id="1f19c-138">Traffic Manager changes the endpoint status to Offline.</span></span> <span data-ttu-id="1f19c-139">To resolve the problem, check the website configuration to ensure that the proper StatusCode can be returned from the probe path.</span><span class="sxs-lookup"><span data-stu-id="1f19c-139">To resolve the problem, check the website configuration to ensure that the proper StatusCode can be returned from the probe path.</span></span> <span data-ttu-id="1f19c-140">Reconfigure the Traffic Manager probe to point to a path that returns a 200.</span><span class="sxs-lookup"><span data-stu-id="1f19c-140">Reconfigure the Traffic Manager probe to point to a path that returns a 200.</span></span>

<span data-ttu-id="1f19c-141">If your probe is using the HTTPS protocol, you may need to disable certificate checking to avoid SSL/TLS errors during your test.</span><span class="sxs-lookup"><span data-stu-id="1f19c-141">If your probe is using the HTTPS protocol, you may need to disable certificate checking to avoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="1f19c-142">The following PowerShell statements disable certificate validation for the current PowerShell session:</span><span class="sxs-lookup"><span data-stu-id="1f19c-142">The following PowerShell statements disable certificate validation for the current PowerShell session:</span></span>

```powershell
add-type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
    ServicePoint srvPoint, X509Certificate certificate,
    WebRequest request, int certificateProblem) {
    return true;
    }
}
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

## <a name="next-steps"></a><span data-ttu-id="1f19c-143">Next Steps</span><span class="sxs-lookup"><span data-stu-id="1f19c-143">Next Steps</span></span>

[<span data-ttu-id="1f19c-144">About Traffic Manager traffic routing methods</span><span class="sxs-lookup"><span data-stu-id="1f19c-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="1f19c-145">What is Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="1f19c-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="1f19c-146">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="1f19c-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="1f19c-147">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="1f19c-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="1f19c-148">Operations on Traffic Manager (REST API Reference)</span><span class="sxs-lookup"><span data-stu-id="1f19c-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="1f19c-149">[Azure Traffic Manager Cmdlets][1]</span><span class="sxs-lookup"><span data-stu-id="1f19c-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx


