
## <a name="faq---reverse-dns-for-your-azure-assigned-ip-address"></a><span data-ttu-id="96843-101">FAQ - Reverse DNS for your Azure-assigned IP address</span><span class="sxs-lookup"><span data-stu-id="96843-101">FAQ - Reverse DNS for your Azure-assigned IP address</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="96843-102">How much do reverse DNS records cost?</span><span class="sxs-lookup"><span data-stu-id="96843-102">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="96843-103">They're free!</span><span class="sxs-lookup"><span data-stu-id="96843-103">They're free!</span></span>  <span data-ttu-id="96843-104">There is no additional cost for reverse DNS records or queries.</span><span class="sxs-lookup"><span data-stu-id="96843-104">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-the-internet"></a><span data-ttu-id="96843-105">Will my reverse DNS records resolve from the internet?</span><span class="sxs-lookup"><span data-stu-id="96843-105">Will my reverse DNS records resolve from the internet?</span></span>

<span data-ttu-id="96843-106">Yes.</span><span class="sxs-lookup"><span data-stu-id="96843-106">Yes.</span></span> <span data-ttu-id="96843-107">Once you set the reverse DNS property for your Cloud Service, Azure manages all the DNS delegations and DNS zones required to ensure that reverse DNS record resolves for all internet users.</span><span class="sxs-lookup"><span data-stu-id="96843-107">Once you set the reverse DNS property for your Cloud Service, Azure manages all the DNS delegations and DNS zones required to ensure that reverse DNS record resolves for all internet users.</span></span>

### <a name="will-a-default-reverse-dns-record-be-created-for-my-cloud-services"></a><span data-ttu-id="96843-108">Will a default reverse DNS record be created for my Cloud Services?</span><span class="sxs-lookup"><span data-stu-id="96843-108">Will a default reverse DNS record be created for my Cloud Services?</span></span>

<span data-ttu-id="96843-109">No.</span><span class="sxs-lookup"><span data-stu-id="96843-109">No.</span></span> <span data-ttu-id="96843-110">Reverse DNS is an opt-in feature.</span><span class="sxs-lookup"><span data-stu-id="96843-110">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="96843-111">No default reverse DNS records are created if you choose not to configure them.</span><span class="sxs-lookup"><span data-stu-id="96843-111">No default reverse DNS records are created if you choose not to configure them.</span></span>

### <a name="what-is-the-format-for-the-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="96843-112">What is the format for the fully-qualified domain name (FQDN)?</span><span class="sxs-lookup"><span data-stu-id="96843-112">What is the format for the fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="96843-113">FQDNs are specified in forward order, and must be terminated by a dot (e.g., "app1.contoso.com.").</span><span class="sxs-lookup"><span data-stu-id="96843-113">FQDNs are specified in forward order, and must be terminated by a dot (e.g., "app1.contoso.com.").</span></span>

### <a name="what-happens-if-the-validation-checks-for-the-reverse-dns-ive-specified-fail"></a><span data-ttu-id="96843-114">What happens if the validation checks for the reverse DNS I've specified fail?</span><span class="sxs-lookup"><span data-stu-id="96843-114">What happens if the validation checks for the reverse DNS I've specified fail?</span></span>

<span data-ttu-id="96843-115">Where the validation for reverse DNS checks fail, the service management operation will fail.</span><span class="sxs-lookup"><span data-stu-id="96843-115">Where the validation for reverse DNS checks fail, the service management operation will fail.</span></span> <span data-ttu-id="96843-116">Please correct the reverse DNS value as required, and retry.</span><span class="sxs-lookup"><span data-stu-id="96843-116">Please correct the reverse DNS value as required, and retry.</span></span>

### <a name="can-i-manage-reverse-dns-for-my-azure-website"></a><span data-ttu-id="96843-117">Can I manage reverse DNS for my Azure Website?</span><span class="sxs-lookup"><span data-stu-id="96843-117">Can I manage reverse DNS for my Azure Website?</span></span>

<span data-ttu-id="96843-118">Reverse DNS is not supported for Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="96843-118">Reverse DNS is not supported for Azure Websites.</span></span> <span data-ttu-id="96843-119">Reverse DNS is supported for Azure PaaS roles and IaaS virtual machines.</span><span class="sxs-lookup"><span data-stu-id="96843-119">Reverse DNS is supported for Azure PaaS roles and IaaS virtual machines.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-cloud-service"></a><span data-ttu-id="96843-120">Can I configure multiple reverse DNS records for my Cloud Service?</span><span class="sxs-lookup"><span data-stu-id="96843-120">Can I configure multiple reverse DNS records for my Cloud Service?</span></span>

<span data-ttu-id="96843-121">No.</span><span class="sxs-lookup"><span data-stu-id="96843-121">No.</span></span> <span data-ttu-id="96843-122">Azure supports a single reverse DNS record for each Azure Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="96843-122">Azure supports a single reverse DNS record for each Azure Cloud Service.</span></span> <span data-ttu-id="96843-123">Each Azure Cloud Service however can have their own reverse DNS record.</span><span class="sxs-lookup"><span data-stu-id="96843-123">Each Azure Cloud Service however can have their own reverse DNS record.</span></span>

### <a name="can-i-send-emails-to-external-domains-from-my-azure-compute-services"></a><span data-ttu-id="96843-124">Can I send emails to external domains from my Azure Compute services?</span><span class="sxs-lookup"><span data-stu-id="96843-124">Can I send emails to external domains from my Azure Compute services?</span></span>

<span data-ttu-id="96843-125">No.</span><span class="sxs-lookup"><span data-stu-id="96843-125">No.</span></span> <span data-ttu-id="96843-126">[Azure Compute services do not support sending emails to external domains](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/).</span><span class="sxs-lookup"><span data-stu-id="96843-126">[Azure Compute services do not support sending emails to external domains](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/).</span></span>
