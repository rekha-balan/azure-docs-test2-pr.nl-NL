### <a name="prerequisites"></a><span data-ttu-id="fdc86-101">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fdc86-101">Prerequisites</span></span>
* <span data-ttu-id="fdc86-102">A Twilio account</span><span class="sxs-lookup"><span data-stu-id="fdc86-102">A Twilio account</span></span>
* <span data-ttu-id="fdc86-103">A verified Twilio phone number that can receive SMS</span><span class="sxs-lookup"><span data-stu-id="fdc86-103">A verified Twilio phone number that can receive SMS</span></span>
* <span data-ttu-id="fdc86-104">A verified Twilio phone number that can send SMS</span><span class="sxs-lookup"><span data-stu-id="fdc86-104">A verified Twilio phone number that can send SMS</span></span>

> [!NOTE]
> <span data-ttu-id="fdc86-105">If you are using a Twilio trial account, you can only send SMS to **verified** phone numbers.</span><span class="sxs-lookup"><span data-stu-id="fdc86-105">If you are using a Twilio trial account, you can only send SMS to **verified** phone numbers.</span></span>  
> 
> 

<span data-ttu-id="fdc86-106">Before you can use your Twilio account in a Logic app, you must authorize the Logic app to connect to your Twilio account.</span><span class="sxs-lookup"><span data-stu-id="fdc86-106">Before you can use your Twilio account in a Logic app, you must authorize the Logic app to connect to your Twilio account.</span></span> <span data-ttu-id="fdc86-107">Fortunately, you can do this easily from within your Logic app on the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fdc86-107">Fortunately, you can do this easily from within your Logic app on the Azure Portal.</span></span> 

<span data-ttu-id="fdc86-108">Here are the steps to authorize your Logic app to connect to your Twilio account:</span><span class="sxs-lookup"><span data-stu-id="fdc86-108">Here are the steps to authorize your Logic app to connect to your Twilio account:</span></span>

1. <span data-ttu-id="fdc86-109">To create a connection to Twilio, in the Logic app designer, select **Show Microsoft managed APIs** in the drop down list then enter *Twilio* in the search box.</span><span class="sxs-lookup"><span data-stu-id="fdc86-109">To create a connection to Twilio, in the Logic app designer, select **Show Microsoft managed APIs** in the drop down list then enter *Twilio* in the search box.</span></span> <span data-ttu-id="fdc86-110">Select the trigger or action you'll like to use:</span><span class="sxs-lookup"><span data-stu-id="fdc86-110">Select the trigger or action you'll like to use:</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-twilio/twilio-0.png)
2. <span data-ttu-id="fdc86-111">If you haven't created any connections to Twilio before, you'll get prompted to provide your Twilio credentials.</span><span class="sxs-lookup"><span data-stu-id="fdc86-111">If you haven't created any connections to Twilio before, you'll get prompted to provide your Twilio credentials.</span></span> <span data-ttu-id="fdc86-112">These credentials will be used to authorize your Logic app to connect to, and access your Twilio account's data:</span><span class="sxs-lookup"><span data-stu-id="fdc86-112">These credentials will be used to authorize your Logic app to connect to, and access your Twilio account's data:</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-twilio/twilio-1.png)  
3. <span data-ttu-id="fdc86-113">You'll need the **Twilio account id** and **Twilio access token**  from the dashboard in Twilio, so log in to your Twilio account now to grab these two pieces of information:</span><span class="sxs-lookup"><span data-stu-id="fdc86-113">You'll need the **Twilio account id** and **Twilio access token**  from the dashboard in Twilio, so log in to your Twilio account now to grab these two pieces of information:</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-twilio/twilio-2.png)  
4. <span data-ttu-id="fdc86-114">Twilio and Logic apps use different names to identify these two pieces of infomation.</span><span class="sxs-lookup"><span data-stu-id="fdc86-114">Twilio and Logic apps use different names to identify these two pieces of infomation.</span></span> <span data-ttu-id="fdc86-115">Here is how you must map them to the Logic apps dialog: ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-twilio/twilio-3.png)</span><span class="sxs-lookup"><span data-stu-id="fdc86-115">Here is how you must map them to the Logic apps dialog: ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-twilio/twilio-3.png)</span></span>  
5. <span data-ttu-id="fdc86-116">Select the **Create connection** button:</span><span class="sxs-lookup"><span data-stu-id="fdc86-116">Select the **Create connection** button:</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-twilio/twilio-4.png)
6. <span data-ttu-id="fdc86-117">Notice the connection has been created and you are now free to proceed with the other steps in your Logic app:</span><span class="sxs-lookup"><span data-stu-id="fdc86-117">Notice the connection has been created and you are now free to proceed with the other steps in your Logic app:</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/connectors-create-api-twilio/twilio-5.png)







