---
title: Testing Azure VM network throughput | Microsoft Docs
description: Learn how to test Azure virtual machine network throughput.
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: ''
ms.assetid: ''
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: steveesp
ms.openlocfilehash: d05bed3b92836bf496804c9d40b5a62a96ffbc3d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549680"
---
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="92452-103">Bandwidth/Throughput testing (NTTTCP)</span><span class="sxs-lookup"><span data-stu-id="92452-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="92452-104">When testing network throughput performance in Azure, it's best to use a tool that targets the network for testing and minimizes the use of other resources that could impact performance.</span><span class="sxs-lookup"><span data-stu-id="92452-104">When testing network throughput performance in Azure, it's best to use a tool that targets the network for testing and minimizes the use of other resources that could impact performance.</span></span> <span data-ttu-id="92452-105">NTTTCP is recommended.</span><span class="sxs-lookup"><span data-stu-id="92452-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="92452-106">Copy the tool to two Azure VMs of the same size.</span><span class="sxs-lookup"><span data-stu-id="92452-106">Copy the tool to two Azure VMs of the same size.</span></span> <span data-ttu-id="92452-107">One VM functions as SENDER and the other as RECEIVER.</span><span class="sxs-lookup"><span data-stu-id="92452-107">One VM functions as SENDER and the other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="92452-108">Deploying VMs for testing</span><span class="sxs-lookup"><span data-stu-id="92452-108">Deploying VMs for testing</span></span>
<span data-ttu-id="92452-109">For the purposes of this test, the two VMs should be in either the same Cloud Service or the same Availability Set so that we can use their internal IPs and exclude the Load Balancers from the test.</span><span class="sxs-lookup"><span data-stu-id="92452-109">For the purposes of this test, the two VMs should be in either the same Cloud Service or the same Availability Set so that we can use their internal IPs and exclude the Load Balancers from the test.</span></span> <span data-ttu-id="92452-110">It is possible to test with the VIP but this kind of testing is outside the scope of this document.</span><span class="sxs-lookup"><span data-stu-id="92452-110">It is possible to test with the VIP but this kind of testing is outside the scope of this document.</span></span>
 
<span data-ttu-id="92452-111">Make a note of the RECEIVER's IP address.</span><span class="sxs-lookup"><span data-stu-id="92452-111">Make a note of the RECEIVER's IP address.</span></span> <span data-ttu-id="92452-112">Let's call that IP "a.b.c.r"</span><span class="sxs-lookup"><span data-stu-id="92452-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="92452-113">Make a note of the number of cores on the VM.</span><span class="sxs-lookup"><span data-stu-id="92452-113">Make a note of the number of cores on the VM.</span></span> <span data-ttu-id="92452-114">Let's call this "\#num\_cores"</span><span class="sxs-lookup"><span data-stu-id="92452-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="92452-115">Run the NTTTCP test for 300 seconds (or 5 minutes) on the sender VM and receiver VM.</span><span class="sxs-lookup"><span data-stu-id="92452-115">Run the NTTTCP test for 300 seconds (or 5 minutes) on the sender VM and receiver VM.</span></span>

<span data-ttu-id="92452-116">Tip: When setting up this test for the first time, you might try a shorter test period to get feedback sooner.</span><span class="sxs-lookup"><span data-stu-id="92452-116">Tip: When setting up this test for the first time, you might try a shorter test period to get feedback sooner.</span></span> <span data-ttu-id="92452-117">Once the tool is working as expected, extend the test period to 300 seconds for the most accurate results.</span><span class="sxs-lookup"><span data-stu-id="92452-117">Once the tool is working as expected, extend the test period to 300 seconds for the most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="92452-118">The sender **and** receiver must specify **the same** test duration parameter (-t).</span><span class="sxs-lookup"><span data-stu-id="92452-118">The sender **and** receiver must specify **the same** test duration parameter (-t).</span></span>

<span data-ttu-id="92452-119">To test a single TCP stream for 10 seconds:</span><span class="sxs-lookup"><span data-stu-id="92452-119">To test a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="92452-120">Receiver parameters: ntttcp -r -t 10 -P 1</span><span class="sxs-lookup"><span data-stu-id="92452-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="92452-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="92452-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="92452-122">The preceding sample should only be used to confirm your configuration.</span><span class="sxs-lookup"><span data-stu-id="92452-122">The preceding sample should only be used to confirm your configuration.</span></span> <span data-ttu-id="92452-123">Valid examples of testing are covered later in this document.</span><span class="sxs-lookup"><span data-stu-id="92452-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="92452-124">Testing VMs running WINDOWS:</span><span class="sxs-lookup"><span data-stu-id="92452-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-the-vms"></a><span data-ttu-id="92452-125">Get NTTTCP onto the VMs.</span><span class="sxs-lookup"><span data-stu-id="92452-125">Get NTTTCP onto the VMs.</span></span>

<span data-ttu-id="92452-126">Download the latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="92452-126">Download the latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="92452-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span><span class="sxs-lookup"><span data-stu-id="92452-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="92452-128">Consider putting NTTTCP in separate folder, like c:\\tools</span><span class="sxs-lookup"><span data-stu-id="92452-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-the-windows-firewall"></a><span data-ttu-id="92452-129">Allow NTTTCP through the Windows firewall</span><span class="sxs-lookup"><span data-stu-id="92452-129">Allow NTTTCP through the Windows firewall</span></span>
<span data-ttu-id="92452-130">On the RECEIVER, create an Allow rule on the Windows Firewall to allow the NTTTCP traffic to arrive.</span><span class="sxs-lookup"><span data-stu-id="92452-130">On the RECEIVER, create an Allow rule on the Windows Firewall to allow the NTTTCP traffic to arrive.</span></span> <span data-ttu-id="92452-131">It's easiest to allow the entire NTTTCP program by name rather than to allow specific TCP ports inbound.</span><span class="sxs-lookup"><span data-stu-id="92452-131">It's easiest to allow the entire NTTTCP program by name rather than to allow specific TCP ports inbound.</span></span>

<span data-ttu-id="92452-132">Allow ntttcp through the Windows Firewall like this:</span><span class="sxs-lookup"><span data-stu-id="92452-132">Allow ntttcp through the Windows Firewall like this:</span></span>

<span data-ttu-id="92452-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="92452-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="92452-134">For example, if you copied ntttcp.exe to the "c:\\tools" folder, this would be the command:</span><span class="sxs-lookup"><span data-stu-id="92452-134">For example, if you copied ntttcp.exe to the "c:\\tools" folder, this would be the command:</span></span> 

<span data-ttu-id="92452-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="92452-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="92452-136">Running NTTTCP tests</span><span class="sxs-lookup"><span data-stu-id="92452-136">Running NTTTCP tests</span></span>

<span data-ttu-id="92452-137">Start NTTTCP on the RECEIVER (**run from CMD**, not from PowerShell):</span><span class="sxs-lookup"><span data-stu-id="92452-137">Start NTTTCP on the RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="92452-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span><span class="sxs-lookup"><span data-stu-id="92452-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="92452-139">If the VM has four cores and an IP address of 10.0.0.4, it would look like this:</span><span class="sxs-lookup"><span data-stu-id="92452-139">If the VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="92452-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="92452-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="92452-141">Start NTTTCP on the SENDER (**run from CMD**, not from PowerShell):</span><span class="sxs-lookup"><span data-stu-id="92452-141">Start NTTTCP on the SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="92452-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="92452-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="92452-143">Wait for the results.</span><span class="sxs-lookup"><span data-stu-id="92452-143">Wait for the results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="92452-144">Testing VMs running LINUX:</span><span class="sxs-lookup"><span data-stu-id="92452-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="92452-145">Use nttcp-for-linux.</span><span class="sxs-lookup"><span data-stu-id="92452-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="92452-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span><span class="sxs-lookup"><span data-stu-id="92452-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="92452-147">On the Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span><span class="sxs-lookup"><span data-stu-id="92452-147">On the Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="92452-148">CentOS - Install Git:</span><span class="sxs-lookup"><span data-stu-id="92452-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="92452-149">Ubuntu - Install Git:</span><span class="sxs-lookup"><span data-stu-id="92452-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="92452-150">Make and Install on both:</span><span class="sxs-lookup"><span data-stu-id="92452-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="92452-151">As in the Windows example, we assume the Linux RECEIVER's IP is 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="92452-151">As in the Windows example, we assume the Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="92452-152">Start NTTTCP-for-Linux on the RECEIVER:</span><span class="sxs-lookup"><span data-stu-id="92452-152">Start NTTTCP-for-Linux on the RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="92452-153">And on the SENDER, run:</span><span class="sxs-lookup"><span data-stu-id="92452-153">And on the SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="92452-154">Test length defaults to 60 seconds if no time parameter is given</span><span class="sxs-lookup"><span data-stu-id="92452-154">Test length defaults to 60 seconds if no time parameter is given</span></span>

## <a name="next-steps"></a><span data-ttu-id="92452-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="92452-155">Next steps</span></span>
* <span data-ttu-id="92452-156">Depending on results, there may be room to [Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span><span class="sxs-lookup"><span data-stu-id="92452-156">Depending on results, there may be room to [Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="92452-157">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="92452-157">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
