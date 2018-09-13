---
title: Create custom DNS records for a web app | Microsoft Docs
description: How to create custom domain DNS records for web app using Azure DNS.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: a2a429873c30f526a0de05d4018f53f3a83bbe28
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562815"
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="23a56-103">Create DNS records for a web app in a custom domain</span><span class="sxs-lookup"><span data-stu-id="23a56-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="23a56-104">You can use Azure DNS to host a custom domain for your web apps.</span><span class="sxs-lookup"><span data-stu-id="23a56-104">You can use Azure DNS to host a custom domain for your web apps.</span></span> <span data-ttu-id="23a56-105">For example, you are creating an Azure web app and you want your users to access it by either using contoso.com, or www.contoso.com as an FQDN.</span><span class="sxs-lookup"><span data-stu-id="23a56-105">For example, you are creating an Azure web app and you want your users to access it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="23a56-106">To do this, you have to create two records:</span><span class="sxs-lookup"><span data-stu-id="23a56-106">To do this, you have to create two records:</span></span>

* <span data-ttu-id="23a56-107">A root "A" record pointing to contoso.com</span><span class="sxs-lookup"><span data-stu-id="23a56-107">A root "A" record pointing to contoso.com</span></span>
* <span data-ttu-id="23a56-108">A "CNAME" record for the www name that points to the A record</span><span class="sxs-lookup"><span data-stu-id="23a56-108">A "CNAME" record for the www name that points to the A record</span></span>

<span data-ttu-id="23a56-109">Keep in mind that if you create an A record for a web app in Azure, the A record must be manually updated if the underlying IP address for the web app changes.</span><span class="sxs-lookup"><span data-stu-id="23a56-109">Keep in mind that if you create an A record for a web app in Azure, the A record must be manually updated if the underlying IP address for the web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="23a56-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="23a56-110">Before you begin</span></span>

<span data-ttu-id="23a56-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate the zone in your registrar to Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="23a56-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate the zone in your registrar to Azure DNS.</span></span>

1. <span data-ttu-id="23a56-112">To create a DNS zone, follow the steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="23a56-112">To create a DNS zone, follow the steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="23a56-113">To delegate your DNS to Azure DNS, follow the steps in [DNS domain delegation](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="23a56-113">To delegate your DNS to Azure DNS, follow the steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="23a56-114">After creating a zone and delegating it to Azure DNS, you can then create records for your custom domain.</span><span class="sxs-lookup"><span data-stu-id="23a56-114">After creating a zone and delegating it to Azure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="23a56-115">1. Create an A record for your custom domain</span><span class="sxs-lookup"><span data-stu-id="23a56-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="23a56-116">An A record is used to map a name to its IP address.</span><span class="sxs-lookup"><span data-stu-id="23a56-116">An A record is used to map a name to its IP address.</span></span> <span data-ttu-id="23a56-117">In the following example we will assign @ as an A record to an IPv4 address:</span><span class="sxs-lookup"><span data-stu-id="23a56-117">In the following example we will assign @ as an A record to an IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="23a56-118">Step 1</span><span class="sxs-lookup"><span data-stu-id="23a56-118">Step 1</span></span>

<span data-ttu-id="23a56-119">Create an A record and assign to a variable $rs</span><span class="sxs-lookup"><span data-stu-id="23a56-119">Create an A record and assign to a variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="23a56-120">Step 2</span><span class="sxs-lookup"><span data-stu-id="23a56-120">Step 2</span></span>

<span data-ttu-id="23a56-121">Add the IPv4 value to the previously created record set "@" using the $rs variable assigned.</span><span class="sxs-lookup"><span data-stu-id="23a56-121">Add the IPv4 value to the previously created record set "@" using the $rs variable assigned.</span></span> <span data-ttu-id="23a56-122">The IPv4 value assigned will be the IP address for your web app.</span><span class="sxs-lookup"><span data-stu-id="23a56-122">The IPv4 value assigned will be the IP address for your web app.</span></span>

<span data-ttu-id="23a56-123">To find the IP address for a web app, follow the steps in [Configure a custom domain name in Azure App Service](../app-service-web/web-sites-custom-domain-name.md#vip).</span><span class="sxs-lookup"><span data-stu-id="23a56-123">To find the IP address for a web app, follow the steps in [Configure a custom domain name in Azure App Service](../app-service-web/web-sites-custom-domain-name.md#vip).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="23a56-124">Step 3</span><span class="sxs-lookup"><span data-stu-id="23a56-124">Step 3</span></span>

<span data-ttu-id="23a56-125">Commit the changes to the record set.</span><span class="sxs-lookup"><span data-stu-id="23a56-125">Commit the changes to the record set.</span></span> <span data-ttu-id="23a56-126">Use `Set-AzureRMDnsRecordSet` to upload the changes to the record set to Azure DNS:</span><span class="sxs-lookup"><span data-stu-id="23a56-126">Use `Set-AzureRMDnsRecordSet` to upload the changes to the record set to Azure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="23a56-127">2. Create a CNAME record for your custom domain</span><span class="sxs-lookup"><span data-stu-id="23a56-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="23a56-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use the following the example to create a CNAME record for contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="23a56-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use the following the example to create a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="23a56-129">Step 1</span><span class="sxs-lookup"><span data-stu-id="23a56-129">Step 1</span></span>

<span data-ttu-id="23a56-130">Open PowerShell and create a new CNAME record set and assign to a variable $rs.</span><span class="sxs-lookup"><span data-stu-id="23a56-130">Open PowerShell and create a new CNAME record set and assign to a variable $rs.</span></span> <span data-ttu-id="23a56-131">This example will create a record set type CNAME with a "time to live" of 600 seconds in DNS zone named "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="23a56-131">This example will create a record set type CNAME with a "time to live" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="23a56-132">The following example is the response.</span><span class="sxs-lookup"><span data-stu-id="23a56-132">The following example is the response.</span></span>

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="23a56-133">Step 2</span><span class="sxs-lookup"><span data-stu-id="23a56-133">Step 2</span></span>

<span data-ttu-id="23a56-134">Once the CNAME record set is created, you need to create an alias value which will point to the web app.</span><span class="sxs-lookup"><span data-stu-id="23a56-134">Once the CNAME record set is created, you need to create an alias value which will point to the web app.</span></span>

<span data-ttu-id="23a56-135">Using the previously assigned variable "$rs" you can use the PowerShell command below to create the alias for the web app contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="23a56-135">Using the previously assigned variable "$rs" you can use the PowerShell command below to create the alias for the web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="23a56-136">The following example is the response.</span><span class="sxs-lookup"><span data-stu-id="23a56-136">The following example is the response.</span></span>

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="23a56-137">Step 3</span><span class="sxs-lookup"><span data-stu-id="23a56-137">Step 3</span></span>

<span data-ttu-id="23a56-138">Commit the changes using the `Set-AzureRMDnsRecordSet` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="23a56-138">Commit the changes using the `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="23a56-139">You can validate the record was created correctly by querying the "www.contoso.com" using nslookup, as shown below:</span><span class="sxs-lookup"><span data-stu-id="23a56-139">You can validate the record was created correctly by querying the "www.contoso.com" using nslookup, as shown below:</span></span>

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="23a56-140">Create an "awverify" record for web apps</span><span class="sxs-lookup"><span data-stu-id="23a56-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="23a56-141">If you decide to use an A record for your web app, you must go through a verification process to ensure you own the custom domain.</span><span class="sxs-lookup"><span data-stu-id="23a56-141">If you decide to use an A record for your web app, you must go through a verification process to ensure you own the custom domain.</span></span> <span data-ttu-id="23a56-142">This verification step is done by creating a special CNAME record named "awverify".</span><span class="sxs-lookup"><span data-stu-id="23a56-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="23a56-143">This section applies to A records only.</span><span class="sxs-lookup"><span data-stu-id="23a56-143">This section applies to A records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="23a56-144">Step 1</span><span class="sxs-lookup"><span data-stu-id="23a56-144">Step 1</span></span>

<span data-ttu-id="23a56-145">Create the "awverify" record.</span><span class="sxs-lookup"><span data-stu-id="23a56-145">Create the "awverify" record.</span></span> <span data-ttu-id="23a56-146">In the example below, we will create the "aweverify" record for contoso.com to verify ownership for the custom domain.</span><span class="sxs-lookup"><span data-stu-id="23a56-146">In the example below, we will create the "aweverify" record for contoso.com to verify ownership for the custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="23a56-147">The following example is the response.</span><span class="sxs-lookup"><span data-stu-id="23a56-147">The following example is the response.</span></span>

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="23a56-148">Step 2</span><span class="sxs-lookup"><span data-stu-id="23a56-148">Step 2</span></span>

<span data-ttu-id="23a56-149">Once the record set "awverify" is created, assign the CNAME record set alias.</span><span class="sxs-lookup"><span data-stu-id="23a56-149">Once the record set "awverify" is created, assign the CNAME record set alias.</span></span> <span data-ttu-id="23a56-150">In the example below, we will assign the CNAMe record set alias to awverify.contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="23a56-150">In the example below, we will assign the CNAMe record set alias to awverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="23a56-151">The following example is the response.</span><span class="sxs-lookup"><span data-stu-id="23a56-151">The following example is the response.</span></span>

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="23a56-152">Step 3</span><span class="sxs-lookup"><span data-stu-id="23a56-152">Step 3</span></span>

<span data-ttu-id="23a56-153">Commit the changes using the `Set-AzureRMDnsRecordSet cmdlet`, as shown in the command below.</span><span class="sxs-lookup"><span data-stu-id="23a56-153">Commit the changes using the `Set-AzureRMDnsRecordSet cmdlet`, as shown in the command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="23a56-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="23a56-154">Next steps</span></span>

<span data-ttu-id="23a56-155">Follow the steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) to configure your web app to use a custom domain.</span><span class="sxs-lookup"><span data-stu-id="23a56-155">Follow the steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) to configure your web app to use a custom domain.</span></span>
