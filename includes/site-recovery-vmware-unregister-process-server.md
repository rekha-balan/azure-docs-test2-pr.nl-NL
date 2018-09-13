<span data-ttu-id="f41ca-101">The steps to unregister a process server differs depending on its connection status with the Configuration Server.</span><span class="sxs-lookup"><span data-stu-id="f41ca-101">The steps to unregister a process server differs depending on its connection status with the Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="f41ca-102">Unregister a process server that is in a connected state</span><span class="sxs-lookup"><span data-stu-id="f41ca-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="f41ca-103">Remote into the process server as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="f41ca-103">Remote into the process server as an Administrator.</span></span>
2. <span data-ttu-id="f41ca-104">Launch the **Control Panel** and open **Programs > Uninstall a program**</span><span class="sxs-lookup"><span data-stu-id="f41ca-104">Launch the **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="f41ca-105">Uninstall a program by the name **Microsoft Azure Site Recovery Configuration/Process Server**</span><span class="sxs-lookup"><span data-stu-id="f41ca-105">Uninstall a program by the name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="f41ca-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span><span class="sxs-lookup"><span data-stu-id="f41ca-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="f41ca-107">Unregister a process server that is in a disconnected state</span><span class="sxs-lookup"><span data-stu-id="f41ca-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="f41ca-108">Use the below steps should be used if there is no way to revive the virtual machine on which the Process Server was installed.</span><span class="sxs-lookup"><span data-stu-id="f41ca-108">Use the below steps should be used if there is no way to revive the virtual machine on which the Process Server was installed.</span></span>

1. <span data-ttu-id="f41ca-109">Log on to your configuration server as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="f41ca-109">Log on to your configuration server as an Administrator.</span></span>
2. <span data-ttu-id="f41ca-110">Open an Administrative command prompt and browse to the directory `%ProgramData%\ASR\home\svsystems\bin`.</span><span class="sxs-lookup"><span data-stu-id="f41ca-110">Open an Administrative command prompt and browse to the directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="f41ca-111">Now run the command.</span><span class="sxs-lookup"><span data-stu-id="f41ca-111">Now run the command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="f41ca-112">This will purge the details of the process server from the system.</span><span class="sxs-lookup"><span data-stu-id="f41ca-112">This will purge the details of the process server from the system.</span></span>
