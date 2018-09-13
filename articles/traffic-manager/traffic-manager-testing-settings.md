---
title: Verify Azure Traffic Manager settings | Microsoft Docs
description: This article will help you verify your Traffic Manager settings
services: traffic-manager
documentationcenter: ''
author: kumudd
manager: timlt
editor: ''
ms.assetid: 2180b640-596e-4fb2-be59-23a38d606d12
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: aadff1806a7cb22347283143563467366e857569
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551282"
---
# <a name="verify-traffic-manager-settings"></a><span data-ttu-id="88e01-103">Verify Traffic Manager settings</span><span class="sxs-lookup"><span data-stu-id="88e01-103">Verify Traffic Manager settings</span></span>

<span data-ttu-id="88e01-104">To test your Traffic Manager settings, you need to have multiple clients, in various locations, from which you can run your tests.</span><span class="sxs-lookup"><span data-stu-id="88e01-104">To test your Traffic Manager settings, you need to have multiple clients, in various locations, from which you can run your tests.</span></span> <span data-ttu-id="88e01-105">Then, bring the endpoints in your Traffic Manager profile down one at a time.</span><span class="sxs-lookup"><span data-stu-id="88e01-105">Then, bring the endpoints in your Traffic Manager profile down one at a time.</span></span>

* <span data-ttu-id="88e01-106">Set the DNS TTL value low so that changes propagate quickly (for example, 30 seconds).</span><span class="sxs-lookup"><span data-stu-id="88e01-106">Set the DNS TTL value low so that changes propagate quickly (for example, 30 seconds).</span></span>
* <span data-ttu-id="88e01-107">Know the IP addresses of your Azure cloud services and websites in the profile you are testing.</span><span class="sxs-lookup"><span data-stu-id="88e01-107">Know the IP addresses of your Azure cloud services and websites in the profile you are testing.</span></span>
* <span data-ttu-id="88e01-108">Use tools that let you resolve a DNS name to an IP address and display that address.</span><span class="sxs-lookup"><span data-stu-id="88e01-108">Use tools that let you resolve a DNS name to an IP address and display that address.</span></span>

<span data-ttu-id="88e01-109">You are checking to see that the DNS names resolve to IP addresses of the endpoints in your profile.</span><span class="sxs-lookup"><span data-stu-id="88e01-109">You are checking to see that the DNS names resolve to IP addresses of the endpoints in your profile.</span></span> <span data-ttu-id="88e01-110">The names should resolve in a manner consistent with the traffic routing method defined in the Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="88e01-110">The names should resolve in a manner consistent with the traffic routing method defined in the Traffic Manager profile.</span></span> <span data-ttu-id="88e01-111">You can use the tools like **nslookup** or **dig** to resolve DNS names.</span><span class="sxs-lookup"><span data-stu-id="88e01-111">You can use the tools like **nslookup** or **dig** to resolve DNS names.</span></span>

<span data-ttu-id="88e01-112">The following examples help you test your Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="88e01-112">The following examples help you test your Traffic Manager profile.</span></span>

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a><span data-ttu-id="88e01-113">Check Traffic Manager profile using nslookup and ipconfig in Windows</span><span class="sxs-lookup"><span data-stu-id="88e01-113">Check Traffic Manager profile using nslookup and ipconfig in Windows</span></span>

1. <span data-ttu-id="88e01-114">Open a command or Windows PowerShell prompt as an administrator.</span><span class="sxs-lookup"><span data-stu-id="88e01-114">Open a command or Windows PowerShell prompt as an administrator.</span></span>
2. <span data-ttu-id="88e01-115">Type `ipconfig /flushdns` to flush the DNS resolver cache.</span><span class="sxs-lookup"><span data-stu-id="88e01-115">Type `ipconfig /flushdns` to flush the DNS resolver cache.</span></span>
3. <span data-ttu-id="88e01-116">Type `nslookup <your Traffic Manager domain name>`.</span><span class="sxs-lookup"><span data-stu-id="88e01-116">Type `nslookup <your Traffic Manager domain name>`.</span></span> <span data-ttu-id="88e01-117">For example, the following command checks the domain name with the prefix *myapp.contoso*</span><span class="sxs-lookup"><span data-stu-id="88e01-117">For example, the following command checks the domain name with the prefix *myapp.contoso*</span></span>

        nslookup myapp.contoso.trafficmanager.net

    <span data-ttu-id="88e01-118">A typical result shows the following information:</span><span class="sxs-lookup"><span data-stu-id="88e01-118">A typical result shows the following information:</span></span>

    + <span data-ttu-id="88e01-119">The DNS name and IP address of the DNS server being accessed to resolve this Traffic Manager domain name.</span><span class="sxs-lookup"><span data-stu-id="88e01-119">The DNS name and IP address of the DNS server being accessed to resolve this Traffic Manager domain name.</span></span>
    + <span data-ttu-id="88e01-120">The Traffic Manager domain name you typed on the command line after "nslookup" and the IP address to which the Traffic Manager domain resolves.</span><span class="sxs-lookup"><span data-stu-id="88e01-120">The Traffic Manager domain name you typed on the command line after "nslookup" and the IP address to which the Traffic Manager domain resolves.</span></span> <span data-ttu-id="88e01-121">The second IP address is the important one to check.</span><span class="sxs-lookup"><span data-stu-id="88e01-121">The second IP address is the important one to check.</span></span> <span data-ttu-id="88e01-122">It should match a public virtual IP (VIP) address for one of the cloud services or websites in the Traffic Manager profile you are testing.</span><span class="sxs-lookup"><span data-stu-id="88e01-122">It should match a public virtual IP (VIP) address for one of the cloud services or websites in the Traffic Manager profile you are testing.</span></span>

## <a name="how-to-test-the-failover-traffic-routing-method"></a><span data-ttu-id="88e01-123">How to test the failover traffic routing method</span><span class="sxs-lookup"><span data-stu-id="88e01-123">How to test the failover traffic routing method</span></span>

1. <span data-ttu-id="88e01-124">Leave all endpoints up.</span><span class="sxs-lookup"><span data-stu-id="88e01-124">Leave all endpoints up.</span></span>
2. <span data-ttu-id="88e01-125">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span><span class="sxs-lookup"><span data-stu-id="88e01-125">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span></span>
3. <span data-ttu-id="88e01-126">Ensure that the resolved IP address matches the primary endpoint.</span><span class="sxs-lookup"><span data-stu-id="88e01-126">Ensure that the resolved IP address matches the primary endpoint.</span></span>
4. <span data-ttu-id="88e01-127">Bring down your primary endpoint or remove the monitoring file so that Traffic Manager thinks that the application is down.</span><span class="sxs-lookup"><span data-stu-id="88e01-127">Bring down your primary endpoint or remove the monitoring file so that Traffic Manager thinks that the application is down.</span></span>
5. <span data-ttu-id="88e01-128">Wait for the DNS Time-to-Live (TTL) of the Traffic Manager profile plus an additional two minutes.</span><span class="sxs-lookup"><span data-stu-id="88e01-128">Wait for the DNS Time-to-Live (TTL) of the Traffic Manager profile plus an additional two minutes.</span></span> <span data-ttu-id="88e01-129">For example, if your DNS TTL is 300 seconds (5 minutes), you must wait for seven minutes.</span><span class="sxs-lookup"><span data-stu-id="88e01-129">For example, if your DNS TTL is 300 seconds (5 minutes), you must wait for seven minutes.</span></span>
6. <span data-ttu-id="88e01-130">Flush your DNS client cache and request DNS resolution using nslookup.</span><span class="sxs-lookup"><span data-stu-id="88e01-130">Flush your DNS client cache and request DNS resolution using nslookup.</span></span> <span data-ttu-id="88e01-131">In Windows, you can flush your DNS cache with the ipconfig /flushdns command.</span><span class="sxs-lookup"><span data-stu-id="88e01-131">In Windows, you can flush your DNS cache with the ipconfig /flushdns command.</span></span>
7. <span data-ttu-id="88e01-132">Ensure that the resolved IP address matches your secondary endpoint.</span><span class="sxs-lookup"><span data-stu-id="88e01-132">Ensure that the resolved IP address matches your secondary endpoint.</span></span>
8. <span data-ttu-id="88e01-133">Repeat the process, bringing down each endpoint in turn.</span><span class="sxs-lookup"><span data-stu-id="88e01-133">Repeat the process, bringing down each endpoint in turn.</span></span> <span data-ttu-id="88e01-134">Verify that the DNS returns the IP address of the next endpoint in the list.</span><span class="sxs-lookup"><span data-stu-id="88e01-134">Verify that the DNS returns the IP address of the next endpoint in the list.</span></span> <span data-ttu-id="88e01-135">When all endpoints are down, you should obtain the IP address of the primary endpoint again.</span><span class="sxs-lookup"><span data-stu-id="88e01-135">When all endpoints are down, you should obtain the IP address of the primary endpoint again.</span></span>

## <a name="how-to-test-the-weighted-traffic-routing-method"></a><span data-ttu-id="88e01-136">How to test the weighted traffic routing method</span><span class="sxs-lookup"><span data-stu-id="88e01-136">How to test the weighted traffic routing method</span></span>

1. <span data-ttu-id="88e01-137">Leave all endpoints up.</span><span class="sxs-lookup"><span data-stu-id="88e01-137">Leave all endpoints up.</span></span>
2. <span data-ttu-id="88e01-138">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span><span class="sxs-lookup"><span data-stu-id="88e01-138">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span></span>
3. <span data-ttu-id="88e01-139">Ensure that the resolved IP address matches one of your endpoints.</span><span class="sxs-lookup"><span data-stu-id="88e01-139">Ensure that the resolved IP address matches one of your endpoints.</span></span>
4. <span data-ttu-id="88e01-140">Flush your DNS client cache and repeat steps 2 and 3 for each endpoint.</span><span class="sxs-lookup"><span data-stu-id="88e01-140">Flush your DNS client cache and repeat steps 2 and 3 for each endpoint.</span></span> <span data-ttu-id="88e01-141">You should see different IP addresses returned for each of your endpoints.</span><span class="sxs-lookup"><span data-stu-id="88e01-141">You should see different IP addresses returned for each of your endpoints.</span></span>

## <a name="how-to-test-the-performance-traffic-routing-method"></a><span data-ttu-id="88e01-142">How to test the performance traffic routing method</span><span class="sxs-lookup"><span data-stu-id="88e01-142">How to test the performance traffic routing method</span></span>

<span data-ttu-id="88e01-143">To effectively test a performance traffic routing method, you must have clients located in different parts of the world.</span><span class="sxs-lookup"><span data-stu-id="88e01-143">To effectively test a performance traffic routing method, you must have clients located in different parts of the world.</span></span> <span data-ttu-id="88e01-144">You can create clients in different Azure regions that can be used to test your services.</span><span class="sxs-lookup"><span data-stu-id="88e01-144">You can create clients in different Azure regions that can be used to test your services.</span></span> <span data-ttu-id="88e01-145">If you have a global network, you can remotely sign in to clients in other parts of the world and run your tests from there.</span><span class="sxs-lookup"><span data-stu-id="88e01-145">If you have a global network, you can remotely sign in to clients in other parts of the world and run your tests from there.</span></span>

<span data-ttu-id="88e01-146">Alternatively, there are free web-based DNS lookup and dig services available.</span><span class="sxs-lookup"><span data-stu-id="88e01-146">Alternatively, there are free web-based DNS lookup and dig services available.</span></span> <span data-ttu-id="88e01-147">Some of these tools give you the ability to check DNS name resolution from various locations around the world.</span><span class="sxs-lookup"><span data-stu-id="88e01-147">Some of these tools give you the ability to check DNS name resolution from various locations around the world.</span></span> <span data-ttu-id="88e01-148">Do a search on "DNS lookup" for examples.</span><span class="sxs-lookup"><span data-stu-id="88e01-148">Do a search on "DNS lookup" for examples.</span></span> <span data-ttu-id="88e01-149">Third-party services like Gomez or Keynote can be used to confirm that your profiles are distributing traffic as expected.</span><span class="sxs-lookup"><span data-stu-id="88e01-149">Third-party services like Gomez or Keynote can be used to confirm that your profiles are distributing traffic as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88e01-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="88e01-150">Next steps</span></span>

* [<span data-ttu-id="88e01-151">About Traffic Manager traffic routing methods</span><span class="sxs-lookup"><span data-stu-id="88e01-151">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="88e01-152">Traffic Manager performance considerations</span><span class="sxs-lookup"><span data-stu-id="88e01-152">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
* [<span data-ttu-id="88e01-153">Troubleshooting Traffic Manager degraded state</span><span class="sxs-lookup"><span data-stu-id="88e01-153">Troubleshooting Traffic Manager degraded state</span></span>](traffic-manager-troubleshooting-degraded.md)
