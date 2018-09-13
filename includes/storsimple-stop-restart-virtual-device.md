#### <a name="to-stop-and-start-a-virtual-device"></a><span data-ttu-id="f6663-101">To stop and start a virtual device</span><span class="sxs-lookup"><span data-stu-id="f6663-101">To stop and start a virtual device</span></span>
<span data-ttu-id="f6663-102">To stop a virtual device, click its name, and then click **Shutdown**.</span><span class="sxs-lookup"><span data-stu-id="f6663-102">To stop a virtual device, click its name, and then click **Shutdown**.</span></span> <span data-ttu-id="f6663-103">While the virtual device is shutting down, its status is **Stopping**.</span><span class="sxs-lookup"><span data-stu-id="f6663-103">While the virtual device is shutting down, its status is **Stopping**.</span></span> <span data-ttu-id="f6663-104">After the virtual device is stopped, its status is **Stopped**.</span><span class="sxs-lookup"><span data-stu-id="f6663-104">After the virtual device is stopped, its status is **Stopped**.</span></span>

<span data-ttu-id="f6663-105">Use the following cmdlets to stop and start a virtual device.</span><span class="sxs-lookup"><span data-stu-id="f6663-105">Use the following cmdlets to stop and start a virtual device.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="to-restart-a-virtual-device"></a><span data-ttu-id="f6663-106">To restart a virtual device</span><span class="sxs-lookup"><span data-stu-id="f6663-106">To restart a virtual device</span></span>
<span data-ttu-id="f6663-107">When a virtual device is running and you want to restart it, click its name, and then click **Restart**.</span><span class="sxs-lookup"><span data-stu-id="f6663-107">When a virtual device is running and you want to restart it, click its name, and then click **Restart**.</span></span> <span data-ttu-id="f6663-108">While the virtual device is restarting, its status is **Restarting**.</span><span class="sxs-lookup"><span data-stu-id="f6663-108">While the virtual device is restarting, its status is **Restarting**.</span></span> <span data-ttu-id="f6663-109">When the virtual device is ready for you to use, its status is **Running**.</span><span class="sxs-lookup"><span data-stu-id="f6663-109">When the virtual device is ready for you to use, its status is **Running**.</span></span>

<span data-ttu-id="f6663-110">Use the following cmdlet to restart a virtual device.</span><span class="sxs-lookup"><span data-stu-id="f6663-110">Use the following cmdlet to restart a virtual device.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

