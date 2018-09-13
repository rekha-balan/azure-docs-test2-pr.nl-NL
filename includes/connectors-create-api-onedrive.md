#### <a name="prerequisites"></a><span data-ttu-id="0ca29-101">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0ca29-101">Prerequisites</span></span>
* <span data-ttu-id="0ca29-102">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="0ca29-102">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="0ca29-103">A [OneDrive](https://www.microsoft.com/store/apps/onedrive/9wzdncrfj1p3) account</span><span class="sxs-lookup"><span data-stu-id="0ca29-103">A [OneDrive](https://www.microsoft.com/store/apps/onedrive/9wzdncrfj1p3) account</span></span> 

<span data-ttu-id="0ca29-104">Before you can use your OneDrive account in a logic app, authorize the logic app to connect to your OneDrive account.</span><span class="sxs-lookup"><span data-stu-id="0ca29-104">Before you can use your OneDrive account in a logic app, authorize the logic app to connect to your OneDrive account.</span></span>  <span data-ttu-id="0ca29-105">You can do this easily within your logic app on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0ca29-105">You can do this easily within your logic app on the Azure portal.</span></span> 

<span data-ttu-id="0ca29-106">Authorize your logic app to connect to your OneDrive account using the following steps:</span><span class="sxs-lookup"><span data-stu-id="0ca29-106">Authorize your logic app to connect to your OneDrive account using the following steps:</span></span>

1. <span data-ttu-id="0ca29-107">Create a logic app.</span><span class="sxs-lookup"><span data-stu-id="0ca29-107">Create a logic app.</span></span> <span data-ttu-id="0ca29-108">In the Logic Apps designer, select **Show Microsoft managed APIs** in the drop down list, and then enter "onedrive" in the search box.</span><span class="sxs-lookup"><span data-stu-id="0ca29-108">In the Logic Apps designer, select **Show Microsoft managed APIs** in the drop down list, and then enter "onedrive" in the search box.</span></span> <span data-ttu-id="0ca29-109">Select one of the triggers or actions:</span><span class="sxs-lookup"><span data-stu-id="0ca29-109">Select one of the triggers or actions:</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="0ca29-110">If you haven't previously created any connections to OneDrive, you are prompted to sign in using your OneDrive credentials:</span><span class="sxs-lookup"><span data-stu-id="0ca29-110">If you haven't previously created any connections to OneDrive, you are prompted to sign in using your OneDrive credentials:</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-onedrive/onedrive-2.png)
3. <span data-ttu-id="0ca29-111">Select **Sign in**, and enter your user name and password.</span><span class="sxs-lookup"><span data-stu-id="0ca29-111">Select **Sign in**, and enter your user name and password.</span></span> <span data-ttu-id="0ca29-112">Select **Sign in**:</span><span class="sxs-lookup"><span data-stu-id="0ca29-112">Select **Sign in**:</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-onedrive/onedrive-3.png)   
   
    <span data-ttu-id="0ca29-113">These credentials are used to authorize your logic app to connect to, and access the data in your OneDrive account.</span><span class="sxs-lookup"><span data-stu-id="0ca29-113">These credentials are used to authorize your logic app to connect to, and access the data in your OneDrive account.</span></span> 
4. <span data-ttu-id="0ca29-114">Select **Yes** to authorize the logic app to use your OneDrive account:</span><span class="sxs-lookup"><span data-stu-id="0ca29-114">Select **Yes** to authorize the logic app to use your OneDrive account:</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-onedrive/onedrive-4.png)   
5. <span data-ttu-id="0ca29-115">Notice the connection has been created.</span><span class="sxs-lookup"><span data-stu-id="0ca29-115">Notice the connection has been created.</span></span> <span data-ttu-id="0ca29-116">Now, proceed with the other steps in your logic app:</span><span class="sxs-lookup"><span data-stu-id="0ca29-116">Now, proceed with the other steps in your logic app:</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-onedrive/onedrive-5.png)






