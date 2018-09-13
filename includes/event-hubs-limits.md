<span data-ttu-id="2f605-101">The following table lists quotas and limits specific to Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="2f605-101">The following table lists quotas and limits specific to Azure Event Hubs.</span></span> <span data-ttu-id="2f605-102">For information about Event Hubs pricing, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="2f605-102">For information about Event Hubs pricing, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

| <span data-ttu-id="2f605-103">Limit</span><span class="sxs-lookup"><span data-stu-id="2f605-103">Limit</span></span> | <span data-ttu-id="2f605-104">Scope</span><span class="sxs-lookup"><span data-stu-id="2f605-104">Scope</span></span> | <span data-ttu-id="2f605-105">Type</span><span class="sxs-lookup"><span data-stu-id="2f605-105">Type</span></span> | <span data-ttu-id="2f605-106">Behavior when exceeded</span><span class="sxs-lookup"><span data-stu-id="2f605-106">Behavior when exceeded</span></span> | <span data-ttu-id="2f605-107">Value</span><span class="sxs-lookup"><span data-stu-id="2f605-107">Value</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="2f605-108">Number of Event Hubs per namespace</span><span class="sxs-lookup"><span data-stu-id="2f605-108">Number of Event Hubs per namespace</span></span> |<span data-ttu-id="2f605-109">Namespace</span><span class="sxs-lookup"><span data-stu-id="2f605-109">Namespace</span></span> |<span data-ttu-id="2f605-110">Static</span><span class="sxs-lookup"><span data-stu-id="2f605-110">Static</span></span> |<span data-ttu-id="2f605-111">Subsequent requests for creation of a new namespace will be rejected.</span><span class="sxs-lookup"><span data-stu-id="2f605-111">Subsequent requests for creation of a new namespace will be rejected.</span></span> |<span data-ttu-id="2f605-112">10</span><span class="sxs-lookup"><span data-stu-id="2f605-112">10</span></span> |
| <span data-ttu-id="2f605-113">Number of partitions per Event Hub</span><span class="sxs-lookup"><span data-stu-id="2f605-113">Number of partitions per Event Hub</span></span> |<span data-ttu-id="2f605-114">Entity</span><span class="sxs-lookup"><span data-stu-id="2f605-114">Entity</span></span> |<span data-ttu-id="2f605-115">Static</span><span class="sxs-lookup"><span data-stu-id="2f605-115">Static</span></span> |- |<span data-ttu-id="2f605-116">32</span><span class="sxs-lookup"><span data-stu-id="2f605-116">32</span></span> |
| <span data-ttu-id="2f605-117">Number of consumer groups per Event Hub</span><span class="sxs-lookup"><span data-stu-id="2f605-117">Number of consumer groups per Event Hub</span></span> |<span data-ttu-id="2f605-118">Entity</span><span class="sxs-lookup"><span data-stu-id="2f605-118">Entity</span></span> |<span data-ttu-id="2f605-119">Static</span><span class="sxs-lookup"><span data-stu-id="2f605-119">Static</span></span> |- |<span data-ttu-id="2f605-120">20</span><span class="sxs-lookup"><span data-stu-id="2f605-120">20</span></span> |
| <span data-ttu-id="2f605-121">Number of AMQP connections per namespace</span><span class="sxs-lookup"><span data-stu-id="2f605-121">Number of AMQP connections per namespace</span></span> |<span data-ttu-id="2f605-122">Namespace</span><span class="sxs-lookup"><span data-stu-id="2f605-122">Namespace</span></span> |<span data-ttu-id="2f605-123">Static</span><span class="sxs-lookup"><span data-stu-id="2f605-123">Static</span></span> |<span data-ttu-id="2f605-124">Subsequent requests for additional connections will be rejected and an exception will be received by the calling code.</span><span class="sxs-lookup"><span data-stu-id="2f605-124">Subsequent requests for additional connections will be rejected and an exception will be received by the calling code.</span></span> |<span data-ttu-id="2f605-125">5,000</span><span class="sxs-lookup"><span data-stu-id="2f605-125">5,000</span></span> |
| <span data-ttu-id="2f605-126">Maximum size of Event Hubs event</span><span class="sxs-lookup"><span data-stu-id="2f605-126">Maximum size of Event Hubs event</span></span>|<span data-ttu-id="2f605-127">System-wide</span><span class="sxs-lookup"><span data-stu-id="2f605-127">System-wide</span></span> |<span data-ttu-id="2f605-128">Static</span><span class="sxs-lookup"><span data-stu-id="2f605-128">Static</span></span> |- |<span data-ttu-id="2f605-129">256KB</span><span class="sxs-lookup"><span data-stu-id="2f605-129">256KB</span></span> |
| <span data-ttu-id="2f605-130">Maximum size of an Event Hub name</span><span class="sxs-lookup"><span data-stu-id="2f605-130">Maximum size of an Event Hub name</span></span> |<span data-ttu-id="2f605-131">Entity</span><span class="sxs-lookup"><span data-stu-id="2f605-131">Entity</span></span> |<span data-ttu-id="2f605-132">Static</span><span class="sxs-lookup"><span data-stu-id="2f605-132">Static</span></span> |- |<span data-ttu-id="2f605-133">50 characters</span><span class="sxs-lookup"><span data-stu-id="2f605-133">50 characters</span></span> |
| <span data-ttu-id="2f605-134">Number of non-epoch receivers per consumer group</span><span class="sxs-lookup"><span data-stu-id="2f605-134">Number of non-epoch receivers per consumer group</span></span> |<span data-ttu-id="2f605-135">Entity</span><span class="sxs-lookup"><span data-stu-id="2f605-135">Entity</span></span> |<span data-ttu-id="2f605-136">Static</span><span class="sxs-lookup"><span data-stu-id="2f605-136">Static</span></span> |- |<span data-ttu-id="2f605-137">5</span><span class="sxs-lookup"><span data-stu-id="2f605-137">5</span></span> |
| <span data-ttu-id="2f605-138">Maximum retention period of event data</span><span class="sxs-lookup"><span data-stu-id="2f605-138">Maximum retention period of event data</span></span> |<span data-ttu-id="2f605-139">Entity</span><span class="sxs-lookup"><span data-stu-id="2f605-139">Entity</span></span> |<span data-ttu-id="2f605-140">Static</span><span class="sxs-lookup"><span data-stu-id="2f605-140">Static</span></span> |- |<span data-ttu-id="2f605-141">1-7 days</span><span class="sxs-lookup"><span data-stu-id="2f605-141">1-7 days</span></span> |
| <span data-ttu-id="2f605-142">Maximum throughput units</span><span class="sxs-lookup"><span data-stu-id="2f605-142">Maximum throughput units</span></span> |<span data-ttu-id="2f605-143">Namespace</span><span class="sxs-lookup"><span data-stu-id="2f605-143">Namespace</span></span> |<span data-ttu-id="2f605-144">Static</span><span class="sxs-lookup"><span data-stu-id="2f605-144">Static</span></span> |<span data-ttu-id="2f605-145">Exceeding the throughput unit limit will cause your data to be throttled and generate a **ServerBusyException**.</span><span class="sxs-lookup"><span data-stu-id="2f605-145">Exceeding the throughput unit limit will cause your data to be throttled and generate a **ServerBusyException**.</span></span> <span data-ttu-id="2f605-146">You can request a larger number of throughput units for a Standard tier by filing a support ticket.</span><span class="sxs-lookup"><span data-stu-id="2f605-146">You can request a larger number of throughput units for a Standard tier by filing a support ticket.</span></span> <span data-ttu-id="2f605-147">Additional throughput units are available in blocks of twenty on a committed purchase basis.</span><span class="sxs-lookup"><span data-stu-id="2f605-147">Additional throughput units are available in blocks of twenty on a committed purchase basis.</span></span> |<span data-ttu-id="2f605-148">20</span><span class="sxs-lookup"><span data-stu-id="2f605-148">20</span></span> |
