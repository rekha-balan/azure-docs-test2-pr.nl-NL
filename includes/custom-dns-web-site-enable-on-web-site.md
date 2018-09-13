<span data-ttu-id="182ab-101">After the records for your domain name have propagated, you must associate them with your Web App.</span><span class="sxs-lookup"><span data-stu-id="182ab-101">After the records for your domain name have propagated, you must associate them with your Web App.</span></span> <span data-ttu-id="182ab-102">Use the following steps to enable the domain names using your web browser.</span><span class="sxs-lookup"><span data-stu-id="182ab-102">Use the following steps to enable the domain names using your web browser.</span></span>

> [!NOTE]
> <span data-ttu-id="182ab-103">It can take some time for TXT records created in the previous steps to propagate through the DNS system.</span><span class="sxs-lookup"><span data-stu-id="182ab-103">It can take some time for TXT records created in the previous steps to propagate through the DNS system.</span></span> <span data-ttu-id="182ab-104">You cannot add the domain name of to your web app until the TXT record has propagated.</span><span class="sxs-lookup"><span data-stu-id="182ab-104">You cannot add the domain name of to your web app until the TXT record has propagated.</span></span> <span data-ttu-id="182ab-105">If you are using an A record, you cannot add the A record domain name to your web app until the TXT record created in the previous step has propagated.</span><span class="sxs-lookup"><span data-stu-id="182ab-105">If you are using an A record, you cannot add the A record domain name to your web app until the TXT record created in the previous step has propagated.</span></span>
> 
> <span data-ttu-id="182ab-106">You can use a service such as <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> to verify that the TXT record is available.</span><span class="sxs-lookup"><span data-stu-id="182ab-106">You can use a service such as <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> to verify that the TXT record is available.</span></span>
> 
> 

1. <span data-ttu-id="182ab-107">In your browser, open the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="182ab-107">In your browser, open the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="182ab-108">In the **Web Apps** tab, click the name of your web app, and then select **Custom domains**</span><span class="sxs-lookup"><span data-stu-id="182ab-108">In the **Web Apps** tab, click the name of your web app, and then select **Custom domains**</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/custom-dns-web-site/dncmntask-cname-6.png)
3. <span data-ttu-id="182ab-109">In the **Custom domains** blade, click **Add hostname**.</span><span class="sxs-lookup"><span data-stu-id="182ab-109">In the **Custom domains** blade, click **Add hostname**.</span></span>
4. <span data-ttu-id="182ab-110">Use the **Hostname** text boxes to enter the domain names to associate with this web app.</span><span class="sxs-lookup"><span data-stu-id="182ab-110">Use the **Hostname** text boxes to enter the domain names to associate with this web app.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/custom-dns-web-site/add-custom-domain.png)
5. <span data-ttu-id="182ab-111">Click **Validate**.</span><span class="sxs-lookup"><span data-stu-id="182ab-111">Click **Validate**.</span></span>
6. <span data-ttu-id="182ab-112">Upon clicking **Validate** Azure will kick off Domain Verification workflow.</span><span class="sxs-lookup"><span data-stu-id="182ab-112">Upon clicking **Validate** Azure will kick off Domain Verification workflow.</span></span> <span data-ttu-id="182ab-113">This will check for Domain ownership as well as Hostname availability and report success or detailed error with prescriptive guidence on how to fix the error.</span><span class="sxs-lookup"><span data-stu-id="182ab-113">This will check for Domain ownership as well as Hostname availability and report success or detailed error with prescriptive guidence on how to fix the error.</span></span>    

<span data-ttu-id="182ab-114">At this point, you should be able to enter the custom domain name in your browser and see that it successfully takes you to your web app.</span><span class="sxs-lookup"><span data-stu-id="182ab-114">At this point, you should be able to enter the custom domain name in your browser and see that it successfully takes you to your web app.</span></span>



