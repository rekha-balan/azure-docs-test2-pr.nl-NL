---
title: Using Dynamic DNS to register hostnames
description: This page gives details on how to set up Dynamic DNS to register hostnames in your own DNS servers.
services: dns
documentationcenter: na
author: GarethBradshawMSFT
manager: timlt
editor: ''
ms.assetid: c315961a-fa33-45cf-82b9-4551e70d32dd
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2017
ms.author: garbrad
ms.openlocfilehash: 440a062e5fff73526b2d77d7d0a7c52ca72a66f1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550206"
---
# <a name="using-dynamic-dns-to-register-hostnames-in-your-own-dns-server"></a><span data-ttu-id="66cc1-103">Using Dynamic DNS to register hostnames in your own DNS server</span><span class="sxs-lookup"><span data-stu-id="66cc1-103">Using Dynamic DNS to register hostnames in your own DNS server</span></span>
<span data-ttu-id="66cc1-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span><span class="sxs-lookup"><span data-stu-id="66cc1-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span></span> <span data-ttu-id="66cc1-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span><span class="sxs-lookup"><span data-stu-id="66cc1-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span></span> <span data-ttu-id="66cc1-106">This gives you the power to tailor your DNS solution to suit your own specific needs.</span><span class="sxs-lookup"><span data-stu-id="66cc1-106">This gives you the power to tailor your DNS solution to suit your own specific needs.</span></span> <span data-ttu-id="66cc1-107">For example, you may need to access on-premises resources via your Active Directory domain controller.</span><span class="sxs-lookup"><span data-stu-id="66cc1-107">For example, you may need to access on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="66cc1-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for the same vnet to Azure to resolve hostnames.</span><span class="sxs-lookup"><span data-stu-id="66cc1-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for the same vnet to Azure to resolve hostnames.</span></span> <span data-ttu-id="66cc1-109">If you do not wish to use this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span><span class="sxs-lookup"><span data-stu-id="66cc1-109">If you do not wish to use this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span></span>  <span data-ttu-id="66cc1-110">Azure doesn't have the ability (e.g. credentials) to directly create records in your DNS servers, so alternative arrangements are often needed.</span><span class="sxs-lookup"><span data-stu-id="66cc1-110">Azure doesn't have the ability (e.g. credentials) to directly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="66cc1-111">Here are some common scenarios with alternatives.</span><span class="sxs-lookup"><span data-stu-id="66cc1-111">Here are some common scenarios with alternatives.</span></span>

## <a name="windows-clients"></a><span data-ttu-id="66cc1-112">Windows clients</span><span class="sxs-lookup"><span data-stu-id="66cc1-112">Windows clients</span></span>
<span data-ttu-id="66cc1-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span><span class="sxs-lookup"><span data-stu-id="66cc1-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span></span> <span data-ttu-id="66cc1-114">The DNS name is the hostname plus the primary DNS suffix.</span><span class="sxs-lookup"><span data-stu-id="66cc1-114">The DNS name is the hostname plus the primary DNS suffix.</span></span> <span data-ttu-id="66cc1-115">Azure leaves the primary DNS suffix blank, but you can set this in the VM, via the [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span><span class="sxs-lookup"><span data-stu-id="66cc1-115">Azure leaves the primary DNS suffix blank, but you can set this in the VM, via the [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span></span>

<span data-ttu-id="66cc1-116">Domain-joined Windows clients register their IP addresses with the domain controller by using secure Dynamic DNS.</span><span class="sxs-lookup"><span data-stu-id="66cc1-116">Domain-joined Windows clients register their IP addresses with the domain controller by using secure Dynamic DNS.</span></span> <span data-ttu-id="66cc1-117">The domain-join process sets the primary DNS suffix on the client and creates and maintains the trust relationship.</span><span class="sxs-lookup"><span data-stu-id="66cc1-117">The domain-join process sets the primary DNS suffix on the client and creates and maintains the trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="66cc1-118">Linux clients</span><span class="sxs-lookup"><span data-stu-id="66cc1-118">Linux clients</span></span>
<span data-ttu-id="66cc1-119">Linux clients generally don't register themselves with the DNS server on startup, they assume the DHCP server does it.</span><span class="sxs-lookup"><span data-stu-id="66cc1-119">Linux clients generally don't register themselves with the DNS server on startup, they assume the DHCP server does it.</span></span> <span data-ttu-id="66cc1-120">Azure's DHCP servers do not have the ability or credentials to register records in your DNS server.</span><span class="sxs-lookup"><span data-stu-id="66cc1-120">Azure's DHCP servers do not have the ability or credentials to register records in your DNS server.</span></span>  <span data-ttu-id="66cc1-121">You can use a tool called *nsupdate*, which is included in the Bind package, to send Dynamic DNS updates.</span><span class="sxs-lookup"><span data-stu-id="66cc1-121">You can use a tool called *nsupdate*, which is included in the Bind package, to send Dynamic DNS updates.</span></span> <span data-ttu-id="66cc1-122">Because the Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on the DNS server.</span><span class="sxs-lookup"><span data-stu-id="66cc1-122">Because the Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on the DNS server.</span></span>

<span data-ttu-id="66cc1-123">You can use the hooks that are provided by the DHCP client to create and maintain the hostname entry in the DNS server.</span><span class="sxs-lookup"><span data-stu-id="66cc1-123">You can use the hooks that are provided by the DHCP client to create and maintain the hostname entry in the DNS server.</span></span> <span data-ttu-id="66cc1-124">During the DHCP cycle, the client executes the scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span><span class="sxs-lookup"><span data-stu-id="66cc1-124">During the DHCP cycle, the client executes the scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="66cc1-125">This can be used to register the new IP address by using *nsupdate*.</span><span class="sxs-lookup"><span data-stu-id="66cc1-125">This can be used to register the new IP address by using *nsupdate*.</span></span> <span data-ttu-id="66cc1-126">For example:</span><span class="sxs-lookup"><span data-stu-id="66cc1-126">For example:</span></span>

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on the primary nic
        if [ "$interface" != "eth0" ]
        then
            return
        fi

        # when we have a new IP, perform nsupdate
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

        
        

<span data-ttu-id="66cc1-127">You can also use the *nsupdate* command to perform secure Dynamic DNS updates.</span><span class="sxs-lookup"><span data-stu-id="66cc1-127">You can also use the *nsupdate* command to perform secure Dynamic DNS updates.</span></span> <span data-ttu-id="66cc1-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span><span class="sxs-lookup"><span data-stu-id="66cc1-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span>  <span data-ttu-id="66cc1-129">The DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with the public part of the key so that it can verify the signature on the request.</span><span class="sxs-lookup"><span data-stu-id="66cc1-129">The DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with the public part of the key so that it can verify the signature on the request.</span></span> <span data-ttu-id="66cc1-130">You must use the *-k* option to provide the key-pair to *nsupdate* in order for the Dynamic DNS update request to be signed.</span><span class="sxs-lookup"><span data-stu-id="66cc1-130">You must use the *-k* option to provide the key-pair to *nsupdate* in order for the Dynamic DNS update request to be signed.</span></span>

<span data-ttu-id="66cc1-131">When you're using a Windows DNS server, you can use Kerberos authentication with the *-g* parameter in *nsupdate* (not available in the Windows version of *nsupdate*).</span><span class="sxs-lookup"><span data-stu-id="66cc1-131">When you're using a Windows DNS server, you can use Kerberos authentication with the *-g* parameter in *nsupdate* (not available in the Windows version of *nsupdate*).</span></span> <span data-ttu-id="66cc1-132">To do this, use *kinit* to load the credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span><span class="sxs-lookup"><span data-stu-id="66cc1-132">To do this, use *kinit* to load the credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span></span> <span data-ttu-id="66cc1-133">Then *nsupdate -g* will pick up the credentials from the cache.</span><span class="sxs-lookup"><span data-stu-id="66cc1-133">Then *nsupdate -g* will pick up the credentials from the cache.</span></span>

<span data-ttu-id="66cc1-134">If needed, you can add a DNS search suffix to your VMs.</span><span class="sxs-lookup"><span data-stu-id="66cc1-134">If needed, you can add a DNS search suffix to your VMs.</span></span> <span data-ttu-id="66cc1-135">The DNS suffix is specified in the */etc/resolv.conf* file.</span><span class="sxs-lookup"><span data-stu-id="66cc1-135">The DNS suffix is specified in the */etc/resolv.conf* file.</span></span> <span data-ttu-id="66cc1-136">Most Linux distros automatically manage the content of this file, so usually you can't edit it.</span><span class="sxs-lookup"><span data-stu-id="66cc1-136">Most Linux distros automatically manage the content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="66cc1-137">However, you can override the suffix by using the DHCP client's *supersede* command.</span><span class="sxs-lookup"><span data-stu-id="66cc1-137">However, you can override the suffix by using the DHCP client's *supersede* command.</span></span> <span data-ttu-id="66cc1-138">To do this, in */etc/dhcp/dhclient.conf*, add:</span><span class="sxs-lookup"><span data-stu-id="66cc1-138">To do this, in */etc/dhcp/dhclient.conf*, add:</span></span>

        supersede domain-name <required-dns-suffix>;

