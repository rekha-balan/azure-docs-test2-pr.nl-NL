---
title: Tutorial - Create custom Azure DNS records for a web app
description: In this tutorial you create custom domain DNS records for web app using Azure DNS.
services: dns
author: vhorne
ms.service: dns
ms.topic: tutorial
ms.date: 7/20/2018
ms.author: victorh
ms.openlocfilehash: 2abe6c11b2a6fe9a9146f5c5689597fe3e29fa82
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44793434"
---
# <a name="tutorial-create-dns-records-in-a-custom-domain-for-a-web-app"></a><span data-ttu-id="76b4c-103">Tutorial: Create DNS records in a custom domain for a web app</span><span class="sxs-lookup"><span data-stu-id="76b4c-103">Tutorial: Create DNS records in a custom domain for a web app</span></span> 

<span data-ttu-id="76b4c-104">You can configure Azure DNS to host a custom domain for your web apps.</span><span class="sxs-lookup"><span data-stu-id="76b4c-104">You can configure Azure DNS to host a custom domain for your web apps.</span></span> <span data-ttu-id="76b4c-105">For example, you can create an Azure web app and have your users access it using either www.contoso.com or contoso.com as a fully qualified domain name (FQDN).</span><span class="sxs-lookup"><span data-stu-id="76b4c-105">For example, you can create an Azure web app and have your users access it using either www.contoso.com or contoso.com as a fully qualified domain name (FQDN).</span></span>

> [!NOTE]
> <span data-ttu-id="76b4c-106">Contoso.com is used as an example throughout this tutorial.</span><span class="sxs-lookup"><span data-stu-id="76b4c-106">Contoso.com is used as an example throughout this tutorial.</span></span> <span data-ttu-id="76b4c-107">Substitute your own domain name for contoso.com.</span><span class="sxs-lookup"><span data-stu-id="76b4c-107">Substitute your own domain name for contoso.com.</span></span>

<span data-ttu-id="76b4c-108">To do this, you have to create three records:</span><span class="sxs-lookup"><span data-stu-id="76b4c-108">To do this, you have to create three records:</span></span>

* <span data-ttu-id="76b4c-109">A root "A" record pointing to contoso.com</span><span class="sxs-lookup"><span data-stu-id="76b4c-109">A root "A" record pointing to contoso.com</span></span>
* <span data-ttu-id="76b4c-110">A root "TXT" record for verification</span><span class="sxs-lookup"><span data-stu-id="76b4c-110">A root "TXT" record for verification</span></span>
* <span data-ttu-id="76b4c-111">A "CNAME" record for the www name that points to the A record</span><span class="sxs-lookup"><span data-stu-id="76b4c-111">A "CNAME" record for the www name that points to the A record</span></span>

<span data-ttu-id="76b4c-112">Keep in mind that if you create an A record for a web app in Azure, the A record must be manually updated if the underlying IP address for the web app changes.</span><span class="sxs-lookup"><span data-stu-id="76b4c-112">Keep in mind that if you create an A record for a web app in Azure, the A record must be manually updated if the underlying IP address for the web app changes.</span></span>

<span data-ttu-id="76b4c-113">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="76b4c-113">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="76b4c-114">Create an A and TXT record for your custom domain</span><span class="sxs-lookup"><span data-stu-id="76b4c-114">Create an A and TXT record for your custom domain</span></span>
> * <span data-ttu-id="76b4c-115">Create a CNAME record for your custom domain</span><span class="sxs-lookup"><span data-stu-id="76b4c-115">Create a CNAME record for your custom domain</span></span>
> * <span data-ttu-id="76b4c-116">Test the new records</span><span class="sxs-lookup"><span data-stu-id="76b4c-116">Test the new records</span></span>
> * <span data-ttu-id="76b4c-117">Add custom host names you your web app</span><span class="sxs-lookup"><span data-stu-id="76b4c-117">Add custom host names you your web app</span></span>
> * <span data-ttu-id="76b4c-118">Test the custom host names</span><span class="sxs-lookup"><span data-stu-id="76b4c-118">Test the custom host names</span></span>


<span data-ttu-id="76b4c-119">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="76b4c-119">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

## <a name="prerequisites"></a><span data-ttu-id="76b4c-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="76b4c-120">Prerequisites</span></span>

- <span data-ttu-id="76b4c-121">[Create an App Service app](../app-service/app-service-web-get-started-html.md), or use an app that you created for another tutorial.</span><span class="sxs-lookup"><span data-stu-id="76b4c-121">[Create an App Service app](../app-service/app-service-web-get-started-html.md), or use an app that you created for another tutorial.</span></span>

- <span data-ttu-id="76b4c-122">Create a DNS zone in Azure DNS, and delegate the zone in your registrar to Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="76b4c-122">Create a DNS zone in Azure DNS, and delegate the zone in your registrar to Azure DNS.</span></span>

   1. <span data-ttu-id="76b4c-123">To create a DNS zone, follow the steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="76b4c-123">To create a DNS zone, follow the steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
   2. <span data-ttu-id="76b4c-124">To delegate your zone to Azure DNS, follow the steps in [DNS domain delegation](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="76b4c-124">To delegate your zone to Azure DNS, follow the steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="76b4c-125">After creating a zone and delegating it to Azure DNS, you can then create records for your custom domain.</span><span class="sxs-lookup"><span data-stu-id="76b4c-125">After creating a zone and delegating it to Azure DNS, you can then create records for your custom domain.</span></span>

## <a name="create-an-a-record-and-txt-record"></a><span data-ttu-id="76b4c-126">Create an A record and TXT record</span><span class="sxs-lookup"><span data-stu-id="76b4c-126">Create an A record and TXT record</span></span>

<span data-ttu-id="76b4c-127">An A record is used to map a name to its IP address.</span><span class="sxs-lookup"><span data-stu-id="76b4c-127">An A record is used to map a name to its IP address.</span></span> <span data-ttu-id="76b4c-128">In the following example, assign "\@" as an A record using your web app IPv4 address.</span><span class="sxs-lookup"><span data-stu-id="76b4c-128">In the following example, assign "\@" as an A record using your web app IPv4 address.</span></span> <span data-ttu-id="76b4c-129">\@ typically represents the root domain.</span><span class="sxs-lookup"><span data-stu-id="76b4c-129">\@ typically represents the root domain.</span></span>

### <a name="get-the-ipv4-address"></a><span data-ttu-id="76b4c-130">Get the IPv4 address</span><span class="sxs-lookup"><span data-stu-id="76b4c-130">Get the IPv4 address</span></span>

<span data-ttu-id="76b4c-131">In the left navigation of the App Services page in the Azure portal, select **Custom domains**.</span><span class="sxs-lookup"><span data-stu-id="76b4c-131">In the left navigation of the App Services page in the Azure portal, select **Custom domains**.</span></span> 

![Custom domain menu](../app-service/./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="76b4c-133">In the **Custom domains** page, copy the app's IPv4 address:</span><span class="sxs-lookup"><span data-stu-id="76b4c-133">In the **Custom domains** page, copy the app's IPv4 address:</span></span>

![Portal navigation to Azure app](../app-service/./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="create-the-a-record"></a><span data-ttu-id="76b4c-135">Create the A record</span><span class="sxs-lookup"><span data-stu-id="76b4c-135">Create the A record</span></span>

```powershell
New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" `
 -ResourceGroupName "MyAzureResourceGroup" -Ttl 600 `
 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "<your web app IP address>")
```

### <a name="create-the-txt-record"></a><span data-ttu-id="76b4c-136">Create the TXT record</span><span class="sxs-lookup"><span data-stu-id="76b4c-136">Create the TXT record</span></span>

<span data-ttu-id="76b4c-137">App Services uses this record only at configuration time to verify that you own the custom domain.</span><span class="sxs-lookup"><span data-stu-id="76b4c-137">App Services uses this record only at configuration time to verify that you own the custom domain.</span></span> <span data-ttu-id="76b4c-138">You can delete this TXT record after your custom domain is validated and configured in App Service.</span><span class="sxs-lookup"><span data-stu-id="76b4c-138">You can delete this TXT record after your custom domain is validated and configured in App Service.</span></span>

```powershell
New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyAzureResourceGroup `
 -Name `"@" -RecordType "txt" -Ttl 600 `
 -DnsRecords (New-AzureRmDnsRecordConfig -Value  "contoso.azurewebsites.net")
```

## <a name="create-the-cname-record"></a><span data-ttu-id="76b4c-139">Create the CNAME record</span><span class="sxs-lookup"><span data-stu-id="76b4c-139">Create the CNAME record</span></span>

<span data-ttu-id="76b4c-140">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use the following example to create a CNAME record for contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="76b4c-140">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use the following example to create a CNAME record for contoso.azurewebsites.net.</span></span>

<span data-ttu-id="76b4c-141">Open Azure PowerShell and create a new CNAME record.</span><span class="sxs-lookup"><span data-stu-id="76b4c-141">Open Azure PowerShell and create a new CNAME record.</span></span> <span data-ttu-id="76b4c-142">This example creates a record set type CNAME with a "time to live" of 600 seconds in DNS zone named "contoso.com" with the alias for the web app contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="76b4c-142">This example creates a record set type CNAME with a "time to live" of 600 seconds in DNS zone named "contoso.com" with the alias for the web app contoso.azurewebsites.net.</span></span>

### <a name="create-the-record"></a><span data-ttu-id="76b4c-143">Create the record</span><span class="sxs-lookup"><span data-stu-id="76b4c-143">Create the record</span></span>

```powershell
New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName "MyAzureResourceGroup" `
 -Name "www" -RecordType "CNAME" -Ttl 600 `
 -DnsRecords (New-AzureRmDnsRecordConfig -cname "contoso.azurewebsites.net")
```

<span data-ttu-id="76b4c-144">The following example is the response:</span><span class="sxs-lookup"><span data-stu-id="76b4c-144">The following example is the response:</span></span>

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

## <a name="test-the-new-records"></a><span data-ttu-id="76b4c-145">Test the new records</span><span class="sxs-lookup"><span data-stu-id="76b4c-145">Test the new records</span></span>

<span data-ttu-id="76b4c-146">You can validate the records were created correctly by querying the "www.contoso.com"  and "contoso.com" using nslookup, as shown below:</span><span class="sxs-lookup"><span data-stu-id="76b4c-146">You can validate the records were created correctly by querying the "www.contoso.com"  and "contoso.com" using nslookup, as shown below:</span></span>

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

> contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    contoso.com
Address:  <ip of web app service>

> set type=txt
> contoso.com

Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
contoso.com text =

        "contoso.azurewebsites.net"
```
## <a name="add-custom-host-names"></a><span data-ttu-id="76b4c-147">Add custom host names</span><span class="sxs-lookup"><span data-stu-id="76b4c-147">Add custom host names</span></span>

<span data-ttu-id="76b4c-148">Now you can add the custom host names to your web app:</span><span class="sxs-lookup"><span data-stu-id="76b4c-148">Now you can add the custom host names to your web app:</span></span>

```powershell
set-AzureRmWebApp `
 -Name contoso `
 -ResourceGroupName MyAzureResourceGroup `
 -HostNames @("contoso.com","www.contoso.com","contoso.azurewebsites.net")
```
## <a name="test-the-custom-host-names"></a><span data-ttu-id="76b4c-149">Test the custom host names</span><span class="sxs-lookup"><span data-stu-id="76b4c-149">Test the custom host names</span></span>

<span data-ttu-id="76b4c-150">Open a browser and browse to `http://www.<your domainname>` and `http://<you domain name>`.</span><span class="sxs-lookup"><span data-stu-id="76b4c-150">Open a browser and browse to `http://www.<your domainname>` and `http://<you domain name>`.</span></span>

> [!NOTE]
> <span data-ttu-id="76b4c-151">Make sure you include the `http://` prefix, otherwise your browser may attempt predict a URL for you!</span><span class="sxs-lookup"><span data-stu-id="76b4c-151">Make sure you include the `http://` prefix, otherwise your browser may attempt predict a URL for you!</span></span>

<span data-ttu-id="76b4c-152">You should see the same page for both URLs.</span><span class="sxs-lookup"><span data-stu-id="76b4c-152">You should see the same page for both URLs.</span></span> <span data-ttu-id="76b4c-153">For example:</span><span class="sxs-lookup"><span data-stu-id="76b4c-153">For example:</span></span>

![Contoso app service](media/dns-web-sites-custom-domain/contoso-app-svc.png)


## <a name="clean-up-resources"></a><span data-ttu-id="76b4c-155">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="76b4c-155">Clean up resources</span></span>

<span data-ttu-id="76b4c-156">When you no longer need the resources created in this tutorial, you can delete the **myresourcegroup** resource group.</span><span class="sxs-lookup"><span data-stu-id="76b4c-156">When you no longer need the resources created in this tutorial, you can delete the **myresourcegroup** resource group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76b4c-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="76b4c-157">Next steps</span></span>

<span data-ttu-id="76b4c-158">Learn how to create Azure DNS private zones.</span><span class="sxs-lookup"><span data-stu-id="76b4c-158">Learn how to create Azure DNS private zones.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="76b4c-159">Get started with Azure DNS private zones using PowerShell</span><span class="sxs-lookup"><span data-stu-id="76b4c-159">Get started with Azure DNS private zones using PowerShell</span></span>](private-dns-getstarted-powershell.md)
