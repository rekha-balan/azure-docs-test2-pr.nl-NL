<span data-ttu-id="5e0d3-101">While it's possible to paste a MongoLab URI into your code, we recommend configuring it in the environment for ease of management.</span><span class="sxs-lookup"><span data-stu-id="5e0d3-101">While it's possible to paste a MongoLab URI into your code, we recommend configuring it in the environment for ease of management.</span></span> <span data-ttu-id="5e0d3-102">This way, if the URI changes, you can update it through the Azure Portal without going to the code.</span><span class="sxs-lookup"><span data-stu-id="5e0d3-102">This way, if the URI changes, you can update it through the Azure Portal without going to the code.</span></span>

1. <span data-ttu-id="5e0d3-103">In the Azure Portal, select **Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="5e0d3-103">In the Azure Portal, select **Web Apps**.</span></span>
2. <span data-ttu-id="5e0d3-104">Click the name of the web app in the Web Apps list.</span><span class="sxs-lookup"><span data-stu-id="5e0d3-104">Click the name of the web app in the Web Apps list.</span></span>  
   ![WebAppEntry][entry-website]  
   <span data-ttu-id="5e0d3-106">The Web App dashboard displays.</span><span class="sxs-lookup"><span data-stu-id="5e0d3-106">The Web App dashboard displays.</span></span>
3. <span data-ttu-id="5e0d3-107">Click **Configure** in the menu bar.</span><span class="sxs-lookup"><span data-stu-id="5e0d3-107">Click **Configure** in the menu bar.</span></span>  
   <span data-ttu-id="5e0d3-108">![WebAppDashboardConfig][focus-mongolab-websitedashboard-config]</span><span class="sxs-lookup"><span data-stu-id="5e0d3-108">![WebAppDashboardConfig][focus-mongolab-websitedashboard-config]</span></span>
4. <span data-ttu-id="5e0d3-109">Scroll down to the Connection Strings section.</span><span class="sxs-lookup"><span data-stu-id="5e0d3-109">Scroll down to the Connection Strings section.</span></span>  
   ![WebAppConnectionStrings][focus-mongolab-websiteconnectionstring]
5. <span data-ttu-id="5e0d3-111">For **Name**, enter MONGOLAB_URI.</span><span class="sxs-lookup"><span data-stu-id="5e0d3-111">For **Name**, enter MONGOLAB_URI.</span></span>
6. <span data-ttu-id="5e0d3-112">For **Value**, paste the connection string we obtained in the previous section.</span><span class="sxs-lookup"><span data-stu-id="5e0d3-112">For **Value**, paste the connection string we obtained in the previous section.</span></span>
7. <span data-ttu-id="5e0d3-113">Select **Custom** in the **Type** drop-down list (instead of the default **SQLAzure**).</span><span class="sxs-lookup"><span data-stu-id="5e0d3-113">Select **Custom** in the **Type** drop-down list (instead of the default **SQLAzure**).</span></span>
8. <span data-ttu-id="5e0d3-114">Click **Save** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="5e0d3-114">Click **Save** on the toolbar.</span></span>  
   <span data-ttu-id="5e0d3-115">![SaveWebApp][button-website-save]</span><span class="sxs-lookup"><span data-stu-id="5e0d3-115">![SaveWebApp][button-website-save]</span></span>

<span data-ttu-id="5e0d3-116">**Note:** Azure adds the **CUSTOMCONNSTR\_** prefix to this variable, which is why the code above references **CUSTOMCONNSTR\_MONGOLAB_URI.**</span><span class="sxs-lookup"><span data-stu-id="5e0d3-116">**Note:** Azure adds the **CUSTOMCONNSTR\_** prefix to this variable, which is why the code above references **CUSTOMCONNSTR\_MONGOLAB_URI.**</span></span>

[entry-website]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-save-connectioninfo-mongolab/entry-website.png
[focus-mongolab-websitedashboard-config]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-save-connectioninfo-mongolab/focus-mongolab-websitedashboard-config.png
[focus-mongolab-websiteconnectionstring]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-save-connectioninfo-mongolab/focus-mongolab-websiteconnectionstring.png
[button-website-save]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-save-connectioninfo-mongolab/button-website-save.png




