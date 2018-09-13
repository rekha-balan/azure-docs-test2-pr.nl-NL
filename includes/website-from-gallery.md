<span data-ttu-id="ff2cb-101">The Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-101">The Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="ff2cb-102">Web apps created from the Azure Marketplace do not require installation of any software other than the browser used to connect to the [Azure Preview Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="ff2cb-102">Web apps created from the Azure Marketplace do not require installation of any software other than the browser used to connect to the [Azure Preview Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> 

<span data-ttu-id="ff2cb-103">In this tutorial, you'll learn:</span><span class="sxs-lookup"><span data-stu-id="ff2cb-103">In this tutorial, you'll learn:</span></span>

* <span data-ttu-id="ff2cb-104">How to create a new web app through the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-104">How to create a new web app through the Azure Marketplace.</span></span>
* <span data-ttu-id="ff2cb-105">How to deploy the web app through the Azure Preview Portal.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-105">How to deploy the web app through the Azure Preview Portal.</span></span>

<span data-ttu-id="ff2cb-106">You'll build a WordPress blog that uses a default template.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-106">You'll build a WordPress blog that uses a default template.</span></span> <span data-ttu-id="ff2cb-107">The following illustration shows the completed application:</span><span class="sxs-lookup"><span data-stu-id="ff2cb-107">The following illustration shows the completed application:</span></span>

![Wordpress blog][13]

> [!NOTE]
> <span data-ttu-id="ff2cb-109">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-109">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ff2cb-110">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-110">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-a-web-app-in-the-portal"></a><span data-ttu-id="ff2cb-111">Create a web app in the portal</span><span class="sxs-lookup"><span data-stu-id="ff2cb-111">Create a web app in the portal</span></span>
1. <span data-ttu-id="ff2cb-112">Log in to the Azure Preview Portal.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-112">Log in to the Azure Preview Portal.</span></span>
2. <span data-ttu-id="ff2cb-113">Open the Azure Marketplace either by clicking the **Marketplace** icon:</span><span class="sxs-lookup"><span data-stu-id="ff2cb-113">Open the Azure Marketplace either by clicking the **Marketplace** icon:</span></span>
   
    ![Marketplace icon][marketplace]
   
    <span data-ttu-id="ff2cb-115">Or by clicking the **New** icon on the upper right of the dashboard, and selecting **Marketplace** at the bottow of the list.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-115">Or by clicking the **New** icon on the upper right of the dashboard, and selecting **Marketplace** at the bottow of the list.</span></span>
   
    ![Create New][5]
3. <span data-ttu-id="ff2cb-117">Select **Web + Mobile**.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-117">Select **Web + Mobile**.</span></span> <span data-ttu-id="ff2cb-118">Search for **WordPress** and click the **WordPress** icon.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-118">Search for **WordPress** and click the **WordPress** icon.</span></span>
   
    ![WordPress from list][7]
4. <span data-ttu-id="ff2cb-120">After reading the description of the WordPress app, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-120">After reading the description of the WordPress app, select **Create**.</span></span>
5. <span data-ttu-id="ff2cb-121">Click on **Web app**, and provide the required values for configuring your web app.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-121">Click on **Web app**, and provide the required values for configuring your web app.</span></span>
   
    ![configure your app][8]
6. <span data-ttu-id="ff2cb-123">Click on **Database**, and provide the required values for configuring your MySQL database.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-123">Click on **Database**, and provide the required values for configuring your MySQL database.</span></span> 
   
    ![configure database][database]
7. <span data-ttu-id="ff2cb-125">Provide a name for a new resource group.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-125">Provide a name for a new resource group.</span></span>
   
    ![Set resource group][groupname]
8. <span data-ttu-id="ff2cb-127">If necessary, click **SUBSCRIPTION**, and specify the subscription to use.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-127">If necessary, click **SUBSCRIPTION**, and specify the subscription to use.</span></span> 
9. <span data-ttu-id="ff2cb-128">When you have finished defining the web app, click **Create**, and wait while the new web app is created.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-128">When you have finished defining the web app, click **Create**, and wait while the new web app is created.</span></span>
   
   <span data-ttu-id="ff2cb-129">When the app has been created, you will see the resource group containing web app and database.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-129">When the app has been created, you will see the resource group containing web app and database.</span></span>
   
   ![show group][resourcegroup]

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="ff2cb-131">Launch and manage your WordPress web app</span><span class="sxs-lookup"><span data-stu-id="ff2cb-131">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="ff2cb-132">Click on your new web app to see details about your app.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-132">Click on your new web app to see details about your app.</span></span>
   
    ![launch dashboard][10]
2. <span data-ttu-id="ff2cb-134">On the **Essentials** page, click either **Browse** or the link under **Url** to open the web app's welcome page.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-134">On the **Essentials** page, click either **Browse** or the link under **Url** to open the web app's welcome page.</span></span>
   
    ![site URL][browse]
3. <span data-ttu-id="ff2cb-136">If you have not installed WordPress, enter the appropriate configuration information required by WordPress and click **Install WordPress** to finalize configuration and open the web app's login page.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-136">If you have not installed WordPress, enter the appropriate configuration information required by WordPress and click **Install WordPress** to finalize configuration and open the web app's login page.</span></span>
4. <span data-ttu-id="ff2cb-137">Click **Login** and enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-137">Click **Login** and enter your credentials.</span></span>  
5. <span data-ttu-id="ff2cb-138">You'll have a new WordPress web app that looks similar to the web app below.</span><span class="sxs-lookup"><span data-stu-id="ff2cb-138">You'll have a new WordPress web app that looks similar to the web app below.</span></span>    
   
    ![your WordPress site][13]

[5]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/website-from-gallery/start-marketplace.png
[6]: ./media/website-from-gallery/wordpressgallery-02.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/website-from-gallery/search-web-app.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/website-from-gallery/set-web-app.png
[9]: ./media/website-from-gallery/wordpressgallery-05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/website-from-gallery/select-web.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/website-from-gallery/wordpressgallery-09.png
[webapps]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/website-from-gallery/selectwebapps.png
[database]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/website-from-gallery/set-db.png
[resourcegroup]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/website-from-gallery/show-rg.png
[browse]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/website-from-gallery/browse-web.png
[marketplace]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/website-from-gallery/marketplace-icon.png
[groupname]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/website-from-gallery/set-rg.png











