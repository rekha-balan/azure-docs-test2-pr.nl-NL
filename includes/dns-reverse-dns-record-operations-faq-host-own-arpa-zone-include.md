
## <a name="faq---hosting-your-arpa-zone-in-azure-dns"></a><span data-ttu-id="7f5b4-101">FAQ - Hosting your ARPA zone in Azure DNS</span><span class="sxs-lookup"><span data-stu-id="7f5b4-101">FAQ - Hosting your ARPA zone in Azure DNS</span></span>

### <a name="can-i-host-arpa-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="7f5b4-102">Can I host ARPA zones for my ISP-assigned IP blocks on Azure DNS?</span><span class="sxs-lookup"><span data-stu-id="7f5b4-102">Can I host ARPA zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="7f5b4-103">Yes.</span><span class="sxs-lookup"><span data-stu-id="7f5b4-103">Yes.</span></span> <span data-ttu-id="7f5b4-104">Hosting the ARPA zones for your own IP ranges in Azure DNS is fully supported.</span><span class="sxs-lookup"><span data-stu-id="7f5b4-104">Hosting the ARPA zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="7f5b4-105">Simply [create the zone in Azure DNS](../articles/dns/dns-getstarted-create-dnszone.md), then work with your ISP to [delegate the zone](../articles/dns/dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="7f5b4-105">Simply [create the zone in Azure DNS](../articles/dns/dns-getstarted-create-dnszone.md), then work with your ISP to [delegate the zone](../articles/dns/dns-domain-delegation.md).</span></span>  <span data-ttu-id="7f5b4-106">You can then manage the PTR records for each reverse lookup in the same way as other record types.</span><span class="sxs-lookup"><span data-stu-id="7f5b4-106">You can then manage the PTR records for each reverse lookup in the same way as other record types.</span></span>

<span data-ttu-id="7f5b4-107">You can also [import an existing reverse lookup zone using the Azure CLI](../articles/dns/dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="7f5b4-107">You can also [import an existing reverse lookup zone using the Azure CLI](../articles/dns/dns-import-export.md).</span></span>

### <a name="how-much-does-hosting-my-arpa-zone-cost"></a><span data-ttu-id="7f5b4-108">How much does hosting my ARPA zone cost?</span><span class="sxs-lookup"><span data-stu-id="7f5b4-108">How much does hosting my ARPA zone cost?</span></span>

<span data-ttu-id="7f5b4-109">Hosting the ARPA zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="7f5b4-109">Hosting the ARPA zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-arpa-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="7f5b4-110">Can I host ARPA zones for both IPv4 and IPv6 addresses in Azure DNS?</span><span class="sxs-lookup"><span data-stu-id="7f5b4-110">Can I host ARPA zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="7f5b4-111">Yes.</span><span class="sxs-lookup"><span data-stu-id="7f5b4-111">Yes.</span></span>
