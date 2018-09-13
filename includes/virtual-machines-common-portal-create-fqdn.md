## <a name="quick-steps"></a><span data-ttu-id="14576-101">Quick steps</span><span class="sxs-lookup"><span data-stu-id="14576-101">Quick steps</span></span>
<span data-ttu-id="14576-102">The article assumes that you have logged in to your subscription in the portal, and created a virtual machine with the available images using the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="14576-102">The article assumes that you have logged in to your subscription in the portal, and created a virtual machine with the available images using the Resource Manager deployment model.</span></span> <span data-ttu-id="14576-103">Follow these steps once your virtual machine starts running.</span><span class="sxs-lookup"><span data-stu-id="14576-103">Follow these steps once your virtual machine starts running.</span></span>

1. <span data-ttu-id="14576-104">Select your virtual machine in the portal.</span><span class="sxs-lookup"><span data-stu-id="14576-104">Select your virtual machine in the portal.</span></span> <span data-ttu-id="14576-105">The DNS name is blank.</span><span class="sxs-lookup"><span data-stu-id="14576-105">The DNS name is blank.</span></span> <span data-ttu-id="14576-106">Click **Public IP address**:</span><span class="sxs-lookup"><span data-stu-id="14576-106">Click **Public IP address**:</span></span>
   
   ![Click Public IP resource in the portal](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-portal-create-fqdn/locatePublicIP.PNG)

2. <span data-ttu-id="14576-108">Enter the desired DNS name label and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="14576-108">Enter the desired DNS name label and then click **Save**.</span></span>
   
   ![Enter a DNS name label for your public IP resource](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-portal-create-fqdn/dnsNameLabel.PNG)
   
   <span data-ttu-id="14576-110">The Public IP resource now shows this new DNS label on its blade.</span><span class="sxs-lookup"><span data-stu-id="14576-110">The Public IP resource now shows this new DNS label on its blade.</span></span>

3. <span data-ttu-id="14576-111">Close the Public IP blades and go back to the VM overview blade in the portal.</span><span class="sxs-lookup"><span data-stu-id="14576-111">Close the Public IP blades and go back to the VM overview blade in the portal.</span></span> <span data-ttu-id="14576-112">After a few seconds, the portal should update your settings.</span><span class="sxs-lookup"><span data-stu-id="14576-112">After a few seconds, the portal should update your settings.</span></span> <span data-ttu-id="14576-113">Verify that the DNS name/FQDN appears next to the IP address for the **Public IP address** resource.</span><span class="sxs-lookup"><span data-stu-id="14576-113">Verify that the DNS name/FQDN appears next to the IP address for the **Public IP address** resource.</span></span>
   
   ![Confirm your new DNS label is set](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/virtual-machines-common-portal-create-fqdn/fqdnCreated.PNG)




