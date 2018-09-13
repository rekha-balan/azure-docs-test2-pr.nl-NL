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
# <a name="bandwidththroughput-testing-ntttcp"></a>Bandwidth/Throughput testing (NTTTCP)

When testing network throughput performance in Azure, it's best to use a tool that targets the network for testing and minimizes the use of other resources that could impact performance. NTTTCP is recommended.

Copy the tool to two Azure VMs of the same size. One VM functions as SENDER and the other as RECEIVER.

#### <a name="deploying-vms-for-testing"></a>Deploying VMs for testing
For the purposes of this test, the two VMs should be in either the same Cloud Service or the same Availability Set so that we can use their internal IPs and exclude the Load Balancers from the test. It is possible to test with the VIP but this kind of testing is outside the scope of this document.
 
Make a note of the RECEIVER's IP address. Let's call that IP "a.b.c.r"

Make a note of the number of cores on the VM. Let's call this "\#num\_cores"
 
Run the NTTTCP test for 300 seconds (or 5 minutes) on the sender VM and receiver VM.

Tip: When setting up this test for the first time, you might try a shorter test period to get feedback sooner. Once the tool is working as expected, extend the test period to 300 seconds for the most accurate results.

> [!NOTE]
> The sender **and** receiver must specify **the same** test duration parameter (-t).

To test a single TCP stream for 10 seconds:

Receiver parameters: ntttcp -r -t 10 -P 1

Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1

> [!NOTE]
> The preceding sample should only be used to confirm your configuration. Valid examples of testing are covered later in this document.

## <a name="testing-vms-running-windows"></a>Testing VMs running WINDOWS:

#### <a name="get-ntttcp-onto-the-vms"></a>Get NTTTCP onto the VMs.

Download the latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769>

Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit

Consider putting NTTTCP in separate folder, like c:\\tools

#### <a name="allow-ntttcp-through-the-windows-firewall"></a>Allow NTTTCP through the Windows firewall
On the RECEIVER, create an Allow rule on the Windows Firewall to allow the NTTTCP traffic to arrive. It's easiest to allow the entire NTTTCP program by name rather than to allow specific TCP ports inbound.

Allow ntttcp through the Windows Firewall like this:

netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

For example, if you copied ntttcp.exe to the "c:\\tools" folder, this would be the command: 

netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

#### <a name="running-ntttcp-tests"></a>Running NTTTCP tests

Start NTTTCP on the RECEIVER (**run from CMD**, not from PowerShell):

ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300

If the VM has four cores and an IP address of 10.0.0.4, it would look like this:

ntttcp -r –m 8,\*,10.0.0.4 -t 300


Start NTTTCP on the SENDER (**run from CMD**, not from PowerShell):

ntttcp -s –m 8,\*,10.0.0.4 -t 300 

Wait for the results.


## <a name="testing-vms-running-linux"></a>Testing VMs running LINUX:

Use nttcp-for-linux. It is available from <https://github.com/Microsoft/ntttcp-for-linux>

On the Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:

CentOS - Install Git:
``` bash
  yum install gcc -y  
  yum install git -y
```
Ubuntu - Install Git:
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
Make and Install on both:
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

As in the Windows example, we assume the Linux RECEIVER's IP is 10.0.0.4

Start NTTTCP-for-Linux on the RECEIVER:

``` bash
ntttcp -r -t 300
```

And on the SENDER, run:

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
Test length defaults to 60 seconds if no time parameter is given

## <a name="next-steps"></a>Next steps
* Depending on results, there may be room to [Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.
* Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)
