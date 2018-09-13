## <a name="azure-dns"></a><span data-ttu-id="49e58-101">Azure DNS</span><span class="sxs-lookup"><span data-stu-id="49e58-101">Azure DNS</span></span>
<span data-ttu-id="49e58-102">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span><span class="sxs-lookup"><span data-stu-id="49e58-102">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span>

| <span data-ttu-id="49e58-103">Property</span><span class="sxs-lookup"><span data-stu-id="49e58-103">Property</span></span> | <span data-ttu-id="49e58-104">Description</span><span class="sxs-lookup"><span data-stu-id="49e58-104">Description</span></span> | <span data-ttu-id="49e58-105">Sample Value</span><span class="sxs-lookup"><span data-stu-id="49e58-105">Sample Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49e58-106">**DNSzones**</span><span class="sxs-lookup"><span data-stu-id="49e58-106">**DNSzones**</span></span> |<span data-ttu-id="49e58-107">Domain zone information to host DNS records of a particular domain</span><span class="sxs-lookup"><span data-stu-id="49e58-107">Domain zone information to host DNS records of a particular domain</span></span> |<span data-ttu-id="49e58-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span><span class="sxs-lookup"><span data-stu-id="49e58-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span></span> |

### <a name="dns-record-sets"></a><span data-ttu-id="49e58-109">DNS record sets</span><span class="sxs-lookup"><span data-stu-id="49e58-109">DNS record sets</span></span>
<span data-ttu-id="49e58-110">DNS zones have a child object named record set.</span><span class="sxs-lookup"><span data-stu-id="49e58-110">DNS zones have a child object named record set.</span></span> <span data-ttu-id="49e58-111">Record sets are a collection of host records by type for a DNS zone.</span><span class="sxs-lookup"><span data-stu-id="49e58-111">Record sets are a collection of host records by type for a DNS zone.</span></span> <span data-ttu-id="49e58-112">Record types are A, AAAA, CNAME, MX, NS, SOA,SRV and TXT.</span><span class="sxs-lookup"><span data-stu-id="49e58-112">Record types are A, AAAA, CNAME, MX, NS, SOA,SRV and TXT.</span></span>

| <span data-ttu-id="49e58-113">Property</span><span class="sxs-lookup"><span data-stu-id="49e58-113">Property</span></span> | <span data-ttu-id="49e58-114">Description</span><span class="sxs-lookup"><span data-stu-id="49e58-114">Description</span></span> | <span data-ttu-id="49e58-115">Sample value</span><span class="sxs-lookup"><span data-stu-id="49e58-115">Sample value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49e58-116">A</span><span class="sxs-lookup"><span data-stu-id="49e58-116">A</span></span> |<span data-ttu-id="49e58-117">IPv4 record type</span><span class="sxs-lookup"><span data-stu-id="49e58-117">IPv4 record type</span></span> |<span data-ttu-id="49e58-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span><span class="sxs-lookup"><span data-stu-id="49e58-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span></span> |
| <span data-ttu-id="49e58-119">AAAA</span><span class="sxs-lookup"><span data-stu-id="49e58-119">AAAA</span></span> |<span data-ttu-id="49e58-120">IPv6 record type</span><span class="sxs-lookup"><span data-stu-id="49e58-120">IPv6 record type</span></span> |<span data-ttu-id="49e58-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span><span class="sxs-lookup"><span data-stu-id="49e58-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span></span> |
| <span data-ttu-id="49e58-122">CNAME</span><span class="sxs-lookup"><span data-stu-id="49e58-122">CNAME</span></span> |<span data-ttu-id="49e58-123">canonical name record type <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="49e58-123">canonical name record type <sup>1</sup></span></span> |<span data-ttu-id="49e58-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span><span class="sxs-lookup"><span data-stu-id="49e58-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span></span> |
| <span data-ttu-id="49e58-125">MX</span><span class="sxs-lookup"><span data-stu-id="49e58-125">MX</span></span> |<span data-ttu-id="49e58-126">mail record type</span><span class="sxs-lookup"><span data-stu-id="49e58-126">mail record type</span></span> |<span data-ttu-id="49e58-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span><span class="sxs-lookup"><span data-stu-id="49e58-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span></span> |
| <span data-ttu-id="49e58-128">NS</span><span class="sxs-lookup"><span data-stu-id="49e58-128">NS</span></span> |<span data-ttu-id="49e58-129">name server record type</span><span class="sxs-lookup"><span data-stu-id="49e58-129">name server record type</span></span> |<span data-ttu-id="49e58-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span><span class="sxs-lookup"><span data-stu-id="49e58-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span></span> |
| <span data-ttu-id="49e58-131">SOA</span><span class="sxs-lookup"><span data-stu-id="49e58-131">SOA</span></span> |<span data-ttu-id="49e58-132">Start of Authority record type <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="49e58-132">Start of Authority record type <sup>2</sup></span></span> |<span data-ttu-id="49e58-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span><span class="sxs-lookup"><span data-stu-id="49e58-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span></span> |
| <span data-ttu-id="49e58-134">SRV</span><span class="sxs-lookup"><span data-stu-id="49e58-134">SRV</span></span> |<span data-ttu-id="49e58-135">service record type</span><span class="sxs-lookup"><span data-stu-id="49e58-135">service record type</span></span> |<span data-ttu-id="49e58-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span><span class="sxs-lookup"><span data-stu-id="49e58-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span></span> |

<span data-ttu-id="49e58-137"><sup>1</sup> only allows one value per record set.</span><span class="sxs-lookup"><span data-stu-id="49e58-137"><sup>1</sup> only allows one value per record set.</span></span>

<span data-ttu-id="49e58-138"><sup>2</sup> only allows one record type SOA per DNS zone.</span><span class="sxs-lookup"><span data-stu-id="49e58-138"><sup>2</sup> only allows one record type SOA per DNS zone.</span></span> 

<span data-ttu-id="49e58-139">Sample of DNS zone in Json format:</span><span class="sxs-lookup"><span data-stu-id="49e58-139">Sample of DNS zone in Json format:</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "newZoneName": {
          "type": "String",
          "metadata": {
              "description": "The name of the DNS zone to be created."
          }
        },
        "newRecordName": {
          "type": "String",
          "defaultValue": "www",
          "metadata": {
              "description": "The name of the DNS record to be created.  The name is relative to the zone, not the FQDN."
          }
        }
      },
      "resources": 
      [
        {
          "type": "microsoft.network/dnszones",
          "name": "[parameters('newZoneName')]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": {
          }
        },
        {
          "type": "microsoft.network/dnszones/a",
          "name": "[concat(parameters('newZoneName'), concat('/', parameters('newRecordName')))]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": 
          {
            "TTL": 3600,
            "ARecords": 
            [
                {
                    "ipv4Address": "1.2.3.4"
                },
                {
                    "ipv4Address": "1.2.3.5"
                }
            ]
          },
          "dependsOn": [
            "[concat('Microsoft.Network/dnszones/', parameters('newZoneName'))]"
          ]
        }
          ]
    }

## <a name="additional-resources"></a><span data-ttu-id="49e58-140">Additional resources</span><span class="sxs-lookup"><span data-stu-id="49e58-140">Additional resources</span></span>
<span data-ttu-id="49e58-141">Read the [REST API documentation for DNS zones ](https://msdn.microsoft.com/library/azure/mt130626.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="49e58-141">Read the [REST API documentation for DNS zones ](https://msdn.microsoft.com/library/azure/mt130626.aspx) for more information.</span></span>

<span data-ttu-id="49e58-142">Read the [REST API documentation for DNS record sets](https://msdn.microsoft.com/library/azure/mt130627.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="49e58-142">Read the [REST API documentation for DNS record sets](https://msdn.microsoft.com/library/azure/mt130627.aspx) for more information.</span></span>

