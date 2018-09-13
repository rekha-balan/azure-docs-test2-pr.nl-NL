---
title: Using dynamic DNS to register hostnames in Azure | Microsoft Docs
description: Learn how to setup dynamic DNS to register hostnames in your own DNS servers.
services: dns
documentationcenter: na
author: subsarma
manager: vitinnan
editor: ''
ms.assetid: c315961a-fa33-45cf-82b9-4551e70d32dd
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2017
ms.author: subsarma
ms.openlocfilehash: bbbce45b7c321fd4934374c76f2a4421b125d46f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44811862"
---
# <a name="use-dynamic-dns-to-register-hostnames-in-your-own-dns-server"></a><span data-ttu-id="86c89-103">Use dynamic DNS to register hostnames in your own DNS server</span><span class="sxs-lookup"><span data-stu-id="86c89-103">Use dynamic DNS to register hostnames in your own DNS server</span></span>

<span data-ttu-id="86c89-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VM) and role instances.</span><span class="sxs-lookup"><span data-stu-id="86c89-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VM) and role instances.</span></span> <span data-ttu-id="86c89-105">When your name resolution needs exceed the capabilities provided by Azure's default DNS, you can provide your own DNS servers.</span><span class="sxs-lookup"><span data-stu-id="86c89-105">When your name resolution needs exceed the capabilities provided by Azure's default DNS, you can provide your own DNS servers.</span></span> <span data-ttu-id="86c89-106">Using your own DNS servers gives you the ability to tailor your DNS solution to suit your own specific needs.</span><span class="sxs-lookup"><span data-stu-id="86c89-106">Using your own DNS servers gives you the ability to tailor your DNS solution to suit your own specific needs.</span></span> <span data-ttu-id="86c89-107">For example, you may need to access on-premises resources via your Active Directory domain controller.</span><span class="sxs-lookup"><span data-stu-id="86c89-107">For example, you may need to access on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="86c89-108">When your custom DNS servers are hosted as Azure VMs, you can forward hostname queries for the same virtual network to Azure to resolve hostnames.</span><span class="sxs-lookup"><span data-stu-id="86c89-108">When your custom DNS servers are hosted as Azure VMs, you can forward hostname queries for the same virtual network to Azure to resolve hostnames.</span></span> <span data-ttu-id="86c89-109">If you do not wish to use this option, you can register your VM hostnames in your DNS server using dynamic DNS (DDNS).</span><span class="sxs-lookup"><span data-stu-id="86c89-109">If you do not wish to use this option, you can register your VM hostnames in your DNS server using dynamic DNS (DDNS).</span></span> <span data-ttu-id="86c89-110">Azure doesn't have the credentials to directly create records in your DNS servers, so alternative arrangements are often needed.</span><span class="sxs-lookup"><span data-stu-id="86c89-110">Azure doesn't have the credentials to directly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="86c89-111">Some common scenarios, with alternatives follow:</span><span class="sxs-lookup"><span data-stu-id="86c89-111">Some common scenarios, with alternatives follow:</span></span>

## <a name="windows-clients"></a><span data-ttu-id="86c89-112">Windows clients</span><span class="sxs-lookup"><span data-stu-id="86c89-112">Windows clients</span></span>
<span data-ttu-id="86c89-113">Non-domain-joined Windows clients attempt unsecured DDNS updates when they boot, or when their IP address changes.</span><span class="sxs-lookup"><span data-stu-id="86c89-113">Non-domain-joined Windows clients attempt unsecured DDNS updates when they boot, or when their IP address changes.</span></span> <span data-ttu-id="86c89-114">The DNS name is the hostname plus the primary DNS suffix.</span><span class="sxs-lookup"><span data-stu-id="86c89-114">The DNS name is the hostname plus the primary DNS suffix.</span></span> <span data-ttu-id="86c89-115">Azure leaves the primary DNS suffix blank, but you can set the suffix in the VM, via the [user interface](https://technet.microsoft.com/library/cc794784.aspx) or [PowerShell](/powershell/module/dnsclient/set-dnsclient).</span><span class="sxs-lookup"><span data-stu-id="86c89-115">Azure leaves the primary DNS suffix blank, but you can set the suffix in the VM, via the [user interface](https://technet.microsoft.com/library/cc794784.aspx) or [PowerShell](/powershell/module/dnsclient/set-dnsclient).</span></span>

<span data-ttu-id="86c89-116">Domain-joined Windows clients register their IP addresses with the domain controller by using secure DDNS.</span><span class="sxs-lookup"><span data-stu-id="86c89-116">Domain-joined Windows clients register their IP addresses with the domain controller by using secure DDNS.</span></span> <span data-ttu-id="86c89-117">The domain-join process sets the primary DNS suffix on the client and creates and maintains the trust relationship.</span><span class="sxs-lookup"><span data-stu-id="86c89-117">The domain-join process sets the primary DNS suffix on the client and creates and maintains the trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="86c89-118">Linux clients</span><span class="sxs-lookup"><span data-stu-id="86c89-118">Linux clients</span></span>
<span data-ttu-id="86c89-119">Linux clients generally don't register themselves with the DNS server on startup, they assume the DHCP server does it.</span><span class="sxs-lookup"><span data-stu-id="86c89-119">Linux clients generally don't register themselves with the DNS server on startup, they assume the DHCP server does it.</span></span> <span data-ttu-id="86c89-120">Azure's DHCP servers do not have the credentials to register records in your DNS server.</span><span class="sxs-lookup"><span data-stu-id="86c89-120">Azure's DHCP servers do not have the credentials to register records in your DNS server.</span></span> <span data-ttu-id="86c89-121">You can use a tool called `nsupdate`, which is included in the Bind package, to send DDNS updates.</span><span class="sxs-lookup"><span data-stu-id="86c89-121">You can use a tool called `nsupdate`, which is included in the Bind package, to send DDNS updates.</span></span> <span data-ttu-id="86c89-122">Because the DDNS protocol is standardized, you can use `nsupdate` even when you're not using Bind on the DNS server.</span><span class="sxs-lookup"><span data-stu-id="86c89-122">Because the DDNS protocol is standardized, you can use `nsupdate` even when you're not using Bind on the DNS server.</span></span>

<span data-ttu-id="86c89-123">You can use the hooks that are provided by the DHCP client to create and maintain the hostname entry in the DNS server.</span><span class="sxs-lookup"><span data-stu-id="86c89-123">You can use the hooks that are provided by the DHCP client to create and maintain the hostname entry in the DNS server.</span></span> <span data-ttu-id="86c89-124">During the DHCP cycle, the client executes the scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span><span class="sxs-lookup"><span data-stu-id="86c89-124">During the DHCP cycle, the client executes the scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="86c89-125">You can use the hooks to register the new IP address using `nsupdate`.</span><span class="sxs-lookup"><span data-stu-id="86c89-125">You can use the hooks to register the new IP address using `nsupdate`.</span></span> <span data-ttu-id="86c89-126">For example:</span><span class="sxs-lookup"><span data-stu-id="86c89-126">For example:</span></span>

```bash
#!/bin/sh
requireddomain=mydomain.local

# only execute on the primary nic
if [ "$interface" != "eth0" ]
then
    return
fi

# When you have a new IP, perform nsupdate
if [ "$reason" = BOUND ] || [ "$reason" = RENEW ] ||
   [ "$reason" = REBIND ] || [ "$reason" = REBOOT ]
then
   host=`hostname`
   nsupdatecmds=/var/tmp/nsupdatecmds
     echo "update delete $host.$requireddomain a" > $nsupdatecmds
     echo "update add $host.$requireddomain 3600 a $new_ip_address" >> $nsupdatecmds
     echo "send" >> $nsupdatecmds

     nsupdate $nsupdatecmds
fi
```

<span data-ttu-id="86c89-127">You can also use the `nsupdate` command to perform secure DDNS updates.</span><span class="sxs-lookup"><span data-stu-id="86c89-127">You can also use the `nsupdate` command to perform secure DDNS updates.</span></span> <span data-ttu-id="86c89-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span><span class="sxs-lookup"><span data-stu-id="86c89-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span> <span data-ttu-id="86c89-129">The DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with the public part of the key, so that it can verify the signature on the request.</span><span class="sxs-lookup"><span data-stu-id="86c89-129">The DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with the public part of the key, so that it can verify the signature on the request.</span></span> <span data-ttu-id="86c89-130">To provide the key-pair to `nsupdate`, use the `-k` option, for the DDNS update request to be signed.</span><span class="sxs-lookup"><span data-stu-id="86c89-130">To provide the key-pair to `nsupdate`, use the `-k` option, for the DDNS update request to be signed.</span></span>

<span data-ttu-id="86c89-131">When you're using a Windows DNS server, you can use Kerberos authentication with the `-g` parameter in `nsupdate`, but it's not available in the Windows version of `nsupdate`.</span><span class="sxs-lookup"><span data-stu-id="86c89-131">When you're using a Windows DNS server, you can use Kerberos authentication with the `-g` parameter in `nsupdate`, but it's not available in the Windows version of `nsupdate`.</span></span> <span data-ttu-id="86c89-132">To use Kerberos, use `kinit` to load the credentials.</span><span class="sxs-lookup"><span data-stu-id="86c89-132">To use Kerberos, use `kinit` to load the credentials.</span></span> <span data-ttu-id="86c89-133">For example, you can load credentials from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)), then `nsupdate -g` picks up the credentials, from the cache.</span><span class="sxs-lookup"><span data-stu-id="86c89-133">For example, you can load credentials from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)), then `nsupdate -g` picks up the credentials, from the cache.</span></span>

<span data-ttu-id="86c89-134">If needed, you can add a DNS search suffix to your VMs.</span><span class="sxs-lookup"><span data-stu-id="86c89-134">If needed, you can add a DNS search suffix to your VMs.</span></span> <span data-ttu-id="86c89-135">The DNS suffix is specified in the */etc/resolv.conf* file.</span><span class="sxs-lookup"><span data-stu-id="86c89-135">The DNS suffix is specified in the */etc/resolv.conf* file.</span></span> <span data-ttu-id="86c89-136">Most Linux distros automatically manage the content of this file, so usually you can't edit it.</span><span class="sxs-lookup"><span data-stu-id="86c89-136">Most Linux distros automatically manage the content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="86c89-137">However, you can override the suffix by using the DHCP client's `supersede` command.</span><span class="sxs-lookup"><span data-stu-id="86c89-137">However, you can override the suffix by using the DHCP client's `supersede` command.</span></span> <span data-ttu-id="86c89-138">To override the suffix, add the following line to the */etc/dhcp/dhclient.conf* file:</span><span class="sxs-lookup"><span data-stu-id="86c89-138">To override the suffix, add the following line to the */etc/dhcp/dhclient.conf* file:</span></span>

```
supersede domain-name <required-dns-suffix>;
```
