
1. <span data-ttu-id="301c9-101">In the **Hybrid connections** blade, click the hybrid connection you just created, then click **Listener Setup**.</span><span class="sxs-lookup"><span data-stu-id="301c9-101">In the **Hybrid connections** blade, click the hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![Click Listener Setup](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="301c9-103">The **Hybrid connection properties** blade opens.</span><span class="sxs-lookup"><span data-stu-id="301c9-103">The **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="301c9-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save the downloaded HybridConnectionManager.msi package, and copy the gateway connection string.</span><span class="sxs-lookup"><span data-stu-id="301c9-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save the downloaded HybridConnectionManager.msi package, and copy the gateway connection string.</span></span>
   
    ![Click here to install](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="301c9-106">From an administrator command prompt, type the following command to start the installer:</span><span class="sxs-lookup"><span data-stu-id="301c9-106">From an administrator command prompt, type the following command to start the installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="301c9-107">After the installer runs, click **Not now**, then browse to the %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in the **User Account Control** dialog.</span><span class="sxs-lookup"><span data-stu-id="301c9-107">After the installer runs, click **Not now**, then browse to the %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in the **User Account Control** dialog.</span></span>
5. <span data-ttu-id="301c9-108">Paste the hybrid connection string that you copied earlier and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="301c9-108">Paste the hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![Installing](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="301c9-110">When the install completes, click **Close**.</span><span class="sxs-lookup"><span data-stu-id="301c9-110">When the install completes, click **Close**.</span></span>
   
    ![Click Close](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="301c9-112">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span><span class="sxs-lookup"><span data-stu-id="301c9-112">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span></span> 
   
    ![Connected Status](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)






