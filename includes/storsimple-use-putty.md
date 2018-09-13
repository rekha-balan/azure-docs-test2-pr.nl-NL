<!--author=SharS last changed: 9/17/15-->

#### <a name="to-connect-through-the-serial-console"></a><span data-ttu-id="5a762-101">To connect through the serial console</span><span class="sxs-lookup"><span data-stu-id="5a762-101">To connect through the serial console</span></span>
1. <span data-ttu-id="5a762-102">Connect your serial cable to the device (directly or through a USB-serial adapter).</span><span class="sxs-lookup"><span data-stu-id="5a762-102">Connect your serial cable to the device (directly or through a USB-serial adapter).</span></span>
2. <span data-ttu-id="5a762-103">Open the **Control Panel**, and then open the **Device Manager**.</span><span class="sxs-lookup"><span data-stu-id="5a762-103">Open the **Control Panel**, and then open the **Device Manager**.</span></span>
3. <span data-ttu-id="5a762-104">Identify the COM port as shown in the following illustration.</span><span class="sxs-lookup"><span data-stu-id="5a762-104">Identify the COM port as shown in the following illustration.</span></span>
   
     ![Connecting through serial console](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. <span data-ttu-id="5a762-106">Start PuTTY.</span><span class="sxs-lookup"><span data-stu-id="5a762-106">Start PuTTY.</span></span> 
5. <span data-ttu-id="5a762-107">In the right pane, change the **Connection type** to **Serial**.</span><span class="sxs-lookup"><span data-stu-id="5a762-107">In the right pane, change the **Connection type** to **Serial**.</span></span>
6. <span data-ttu-id="5a762-108">In the right pane, type the appropriate COM port.</span><span class="sxs-lookup"><span data-stu-id="5a762-108">In the right pane, type the appropriate COM port.</span></span> <span data-ttu-id="5a762-109">Make sure that the serial configuration parameters are set as follows:</span><span class="sxs-lookup"><span data-stu-id="5a762-109">Make sure that the serial configuration parameters are set as follows:</span></span>
   
   * <span data-ttu-id="5a762-110">Speed: 115,200</span><span class="sxs-lookup"><span data-stu-id="5a762-110">Speed: 115,200</span></span>
   * <span data-ttu-id="5a762-111">Data bits: 8</span><span class="sxs-lookup"><span data-stu-id="5a762-111">Data bits: 8</span></span>
   * <span data-ttu-id="5a762-112">Stop bits: 1</span><span class="sxs-lookup"><span data-stu-id="5a762-112">Stop bits: 1</span></span>
   * <span data-ttu-id="5a762-113">Parity: None</span><span class="sxs-lookup"><span data-stu-id="5a762-113">Parity: None</span></span>
   * <span data-ttu-id="5a762-114">Flow control: None</span><span class="sxs-lookup"><span data-stu-id="5a762-114">Flow control: None</span></span>
     
     <span data-ttu-id="5a762-115">These settings are shown in the following illustration.</span><span class="sxs-lookup"><span data-stu-id="5a762-115">These settings are shown in the following illustration.</span></span>
     
     ![PuTTY settings](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > <span data-ttu-id="5a762-117">If the default flow control setting does not work, try setting the flow control to XON/XOFF.</span><span class="sxs-lookup"><span data-stu-id="5a762-117">If the default flow control setting does not work, try setting the flow control to XON/XOFF.</span></span>
     > 
     > 
7. <span data-ttu-id="5a762-118">Click **Open** to start a serial session.</span><span class="sxs-lookup"><span data-stu-id="5a762-118">Click **Open** to start a serial session.</span></span>



