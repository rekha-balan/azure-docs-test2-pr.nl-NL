## <a name="overview"></a><span data-ttu-id="1649a-101">Overview</span><span class="sxs-lookup"><span data-stu-id="1649a-101">Overview</span></span>

<span data-ttu-id="1649a-102">In this tutorial, you complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="1649a-102">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="1649a-103">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1649a-103">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="1649a-104">This step automatically deploys and configures multiple Azure services.</span><span class="sxs-lookup"><span data-stu-id="1649a-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="1649a-105">Set up your device to communicate with your computer and the remote monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="1649a-105">Set up your device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="1649a-106">Update the sample device code to connect to the remote monitoring solution, and send simulated telemetry that you can view on the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="1649a-106">Update the sample device code to connect to the remote monitoring solution, and send simulated telemetry that you can view on the solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1649a-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1649a-107">Prerequisites</span></span>

<span data-ttu-id="1649a-108">To complete this tutorial, you need an active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1649a-108">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="1649a-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="1649a-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1649a-110">For details, see [Azure Free Trial][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="1649a-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="1649a-111">Required software</span><span class="sxs-lookup"><span data-stu-id="1649a-111">Required software</span></span>

<span data-ttu-id="1649a-112">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="1649a-112">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="1649a-113">Windows does not include an SSH client.</span><span class="sxs-lookup"><span data-stu-id="1649a-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="1649a-114">We recommend using [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="1649a-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="1649a-115">Most Linux distributions and Mac OS include the command-line SSH utility.</span><span class="sxs-lookup"><span data-stu-id="1649a-115">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="1649a-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="1649a-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="1649a-117">Required hardware</span><span class="sxs-lookup"><span data-stu-id="1649a-117">Required hardware</span></span>

<span data-ttu-id="1649a-118">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="1649a-118">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span></span>

<span data-ttu-id="1649a-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span><span class="sxs-lookup"><span data-stu-id="1649a-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="1649a-120">This tutorial uses the following items from the kit:</span><span class="sxs-lookup"><span data-stu-id="1649a-120">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="1649a-121">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="1649a-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="1649a-122">MicroSD Card (with NOOBS)</span><span class="sxs-lookup"><span data-stu-id="1649a-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="1649a-123">A USB Mini cable</span><span class="sxs-lookup"><span data-stu-id="1649a-123">A USB Mini cable</span></span>
- <span data-ttu-id="1649a-124">An Ethernet cable</span><span class="sxs-lookup"><span data-stu-id="1649a-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/