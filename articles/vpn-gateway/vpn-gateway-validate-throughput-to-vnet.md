---
title: Validate VPN throughput to a Microsoft Azure Virtual Network | Microsoft Docs
description: The purpose of this document is to help a user validate the network throughput from their on-premises resources to an Azure virtual machine.
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: ''
tags: azure-resource-manager,azure-service-management
ms.assetid: ''
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: ab8bc304785b5c4f102f1e18a24a3cfcf6f6af10
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550238"
---
# <a name="how-to-validate-vpn-throughput-to-a-virtual-network"></a><span data-ttu-id="1eb3f-103">How to validate VPN throughput to a virtual network</span><span class="sxs-lookup"><span data-stu-id="1eb3f-103">How to validate VPN throughput to a virtual network</span></span>

<span data-ttu-id="1eb3f-104">A VPN gateway connection enables you to establish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-104">A VPN gateway connection enables you to establish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="1eb3f-105">This article shows how to validate network throughput from the on-premises resources to an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-105">This article shows how to validate network throughput from the on-premises resources to an Azure virtual machine.</span></span> <span data-ttu-id="1eb3f-106">It also provides troubleshooting guidance.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="1eb3f-107">This article is intended to help diagnose and fix common issues.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-107">This article is intended to help diagnose and fix common issues.</span></span> <span data-ttu-id="1eb3f-108">If you're unable to solve the issue by using the following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="1eb3f-108">If you're unable to solve the issue by using the following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="1eb3f-109">Overview</span><span class="sxs-lookup"><span data-stu-id="1eb3f-109">Overview</span></span>

<span data-ttu-id="1eb3f-110">The VPN gateway connection involves the following components:</span><span class="sxs-lookup"><span data-stu-id="1eb3f-110">The VPN gateway connection involves the following components:</span></span>

- <span data-ttu-id="1eb3f-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="1eb3f-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="1eb3f-112">Public Internet</span><span class="sxs-lookup"><span data-stu-id="1eb3f-112">Public Internet</span></span>
- <span data-ttu-id="1eb3f-113">Azure VPN gateway</span><span class="sxs-lookup"><span data-stu-id="1eb3f-113">Azure VPN gateway</span></span>
- <span data-ttu-id="1eb3f-114">Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="1eb3f-114">Azure virtual machine</span></span>

<span data-ttu-id="1eb3f-115">The following diagram shows the logical connectivity of an on-premises network to an Azure virtual network through VPN.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-115">The following diagram shows the logical connectivity of an on-premises network to an Azure virtual network through VPN.</span></span>

![Logical Connectivity of Customer Network to MSFT Network using VPN](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-the-maximum-expected-ingressegress"></a><span data-ttu-id="1eb3f-117">Calculate the maximum expected ingress/egress</span><span class="sxs-lookup"><span data-stu-id="1eb3f-117">Calculate the maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="1eb3f-118">Determine your application's baseline throughput requirements.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="1eb3f-119">Determine your Azure VPN gateway throughput limits.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="1eb3f-120">For help, see the "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span><span class="sxs-lookup"><span data-stu-id="1eb3f-120">For help, see the "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="1eb3f-121">Determine the [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-121">Determine the [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="1eb3f-122">Determine your Internet Service Provider (ISP) bandwidth.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="1eb3f-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) \* 0.8.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) \* 0.8.</span></span>

<span data-ttu-id="1eb3f-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need to increase the bandwidth of the resource that you identified as the bottleneck.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need to increase the bandwidth of the resource that you identified as the bottleneck.</span></span> <span data-ttu-id="1eb3f-125">To resize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="1eb3f-125">To resize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="1eb3f-126">To resize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="1eb3f-126">To resize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="1eb3f-127">If you are not experiencing expected Internet bandwidth, you may also want to contact your ISP.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-127">If you are not experiencing expected Internet bandwidth, you may also want to contact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="1eb3f-128">Validate network throughput by using performance tools</span><span class="sxs-lookup"><span data-stu-id="1eb3f-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="1eb3f-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="1eb3f-130">The tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-130">The tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="1eb3f-131">It is limited to 3 Gbps for Windows VMs.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-131">It is limited to 3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="1eb3f-132">This tool does not perform any read/write operations to disk.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-132">This tool does not perform any read/write operations to disk.</span></span> <span data-ttu-id="1eb3f-133">It solely produces self-generated TCP traffic from one end to the other.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-133">It solely produces self-generated TCP traffic from one end to the other.</span></span> <span data-ttu-id="1eb3f-134">It generated statistics based on experimentation that measures the bandwidth available between client and server nodes.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-134">It generated statistics based on experimentation that measures the bandwidth available between client and server nodes.</span></span> <span data-ttu-id="1eb3f-135">When testing between two nodes, one acts as the server and the other as a client.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-135">When testing between two nodes, one acts as the server and the other as a client.</span></span> <span data-ttu-id="1eb3f-136">Once this test is completed, we recommend that you reverse the roles to test both upload and download throughput on both nodes.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-136">Once this test is completed, we recommend that you reverse the roles to test both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="1eb3f-137">Download iPerf</span><span class="sxs-lookup"><span data-stu-id="1eb3f-137">Download iPerf</span></span>
<span data-ttu-id="1eb3f-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span><span class="sxs-lookup"><span data-stu-id="1eb3f-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="1eb3f-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span><span class="sxs-lookup"><span data-stu-id="1eb3f-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="1eb3f-140">The third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-140">The third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="1eb3f-141">Microsoft makes no warranty, implied or otherwise, about the performance or reliability of these products.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-141">Microsoft makes no warranty, implied or otherwise, about the performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="1eb3f-142">Run iPerf (iperf3.exe)</span><span class="sxs-lookup"><span data-stu-id="1eb3f-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="1eb3f-143">Enable an NSG/ACL rule allowing the traffic (for public IP address testing on Azure VM).</span><span class="sxs-lookup"><span data-stu-id="1eb3f-143">Enable an NSG/ACL rule allowing the traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="1eb3f-144">On both nodes, enable a firewall exception for port 5001.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="1eb3f-145">**Windows:** Run the following command as an administrator:</span><span class="sxs-lookup"><span data-stu-id="1eb3f-145">**Windows:** Run the following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="1eb3f-146">To remove the rule when testing is complete, run this command:</span><span class="sxs-lookup"><span data-stu-id="1eb3f-146">To remove the rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="1eb3f-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="1eb3f-148">If there is an application listening on a port, the traffic is allowed through.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-148">If there is an application listening on a port, the traffic is allowed through.</span></span> <span data-ttu-id="1eb3f-149">Custom images that are secured may need ports opened explicitly.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="1eb3f-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="1eb3f-151">On the server node, change to the directory where iperf3.exe is extracted.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-151">On the server node, change to the directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="1eb3f-152">Then run iPerf in server mode and set it to listen on port 5001 as the following commands:</span><span class="sxs-lookup"><span data-stu-id="1eb3f-152">Then run iPerf in server mode and set it to listen on port 5001 as the following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="1eb3f-153">On the client node, change to the directory where iperf tool is extracted and then run the following command:</span><span class="sxs-lookup"><span data-stu-id="1eb3f-153">On the client node, change to the directory where iperf tool is extracted and then run the following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of the iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="1eb3f-154">The client is inducing traffic on port 5001 to the server for 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-154">The client is inducing traffic on port 5001 to the server for 30 seconds.</span></span> <span data-ttu-id="1eb3f-155">The flag '-P ' that indicates we are using 32 simultaneous connections to the server node.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-155">The flag '-P ' that indicates we are using 32 simultaneous connections to the server node.</span></span>

    <span data-ttu-id="1eb3f-156">The following screen shows the output from this example:</span><span class="sxs-lookup"><span data-stu-id="1eb3f-156">The following screen shows the output from this example:</span></span>

    ![Output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="1eb3f-158">(OPTIONAL) To preserve the testing results, run this command:</span><span class="sxs-lookup"><span data-stu-id="1eb3f-158">(OPTIONAL) To preserve the testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="1eb3f-159">After completing the previous steps, execute the same steps with the roles reversed, so that the server node will now be the client and vice-versa.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-159">After completing the previous steps, execute the same steps with the roles reversed, so that the server node will now be the client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="1eb3f-160">Address slow file copy issues</span><span class="sxs-lookup"><span data-stu-id="1eb3f-160">Address slow file copy issues</span></span>
<span data-ttu-id="1eb3f-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="1eb3f-162">This problem is normally due to one or both of the following factors:</span><span class="sxs-lookup"><span data-stu-id="1eb3f-162">This problem is normally due to one or both of the following factors:</span></span>

- <span data-ttu-id="1eb3f-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="1eb3f-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) to copy files by using 16 or 32 threads.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) to copy files by using 16 or 32 threads.</span></span> <span data-ttu-id="1eb3f-165">To change the thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-165">To change the thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br>
<span data-ttu-id="1eb3f-166">![Slow file copy issues](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-validate-throughput-to-vnet/RichCopy.png)</span><span class="sxs-lookup"><span data-stu-id="1eb3f-166">![Slow file copy issues](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-validate-throughput-to-vnet/RichCopy.png)</span></span><br>
- <span data-ttu-id="1eb3f-167">Insufficient VM disk read/write speed.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="1eb3f-168">For more information, see [Azure Storage Troubleshooting](../storage/storage-e2e-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1eb3f-168">For more information, see [Azure Storage Troubleshooting](../storage/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="1eb3f-169">On-premises device external facing interface</span><span class="sxs-lookup"><span data-stu-id="1eb3f-169">On-premises device external facing interface</span></span>
<span data-ttu-id="1eb3f-170">If the on-premises VPN device Internet-facing IP address is included in the [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability to bring up the VPN, sporadic disconnects, or performance issues.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-170">If the on-premises VPN device Internet-facing IP address is included in the [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability to bring up the VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="1eb3f-171">Checking latency</span><span class="sxs-lookup"><span data-stu-id="1eb3f-171">Checking latency</span></span>
<span data-ttu-id="1eb3f-172">Use tracert to trace to Microsoft Azure Edge device to determine if there are any delays exceeding 100 ms between hops.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-172">Use tracert to trace to Microsoft Azure Edge device to determine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="1eb3f-173">From the on-premises network, run *tracert* to the VIP of the Azure Gateway or VM.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-173">From the on-premises network, run *tracert* to the VIP of the Azure Gateway or VM.</span></span> <span data-ttu-id="1eb3f-174">Once you see only \* returned, you know you have reached the Azure edge.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-174">Once you see only \* returned, you know you have reached the Azure edge.</span></span> <span data-ttu-id="1eb3f-175">When you see DNS names that include "MSN" returned, you know you have reached the Microsoft backbone.</span><span class="sxs-lookup"><span data-stu-id="1eb3f-175">When you see DNS names that include "MSN" returned, you know you have reached the Microsoft backbone.</span></span><br><br>
<span data-ttu-id="1eb3f-176">![Checking Latency](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="1eb3f-176">![Checking Latency](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="1eb3f-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="1eb3f-177">Next steps</span></span>
<span data-ttu-id="1eb3f-178">For more information or help, check out the following links:</span><span class="sxs-lookup"><span data-stu-id="1eb3f-178">For more information or help, check out the following links:</span></span>

- [<span data-ttu-id="1eb3f-179">Optimize network throughput for Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="1eb3f-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="1eb3f-180">Microsoft Support</span><span class="sxs-lookup"><span data-stu-id="1eb3f-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)




