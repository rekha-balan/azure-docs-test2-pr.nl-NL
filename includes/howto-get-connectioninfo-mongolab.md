<span data-ttu-id="86e80-101">When you provision a MongoLab database, MongoLab transmits a connection URI to Azure in MongoDB's standard connection string format.</span><span class="sxs-lookup"><span data-stu-id="86e80-101">When you provision a MongoLab database, MongoLab transmits a connection URI to Azure in MongoDB's standard connection string format.</span></span> <span data-ttu-id="86e80-102">This value is used to initiate a MongoDB connection through your choice of MongoDB driver.</span><span class="sxs-lookup"><span data-stu-id="86e80-102">This value is used to initiate a MongoDB connection through your choice of MongoDB driver.</span></span> <span data-ttu-id="86e80-103">For more information about connection strings, see [Connections](http://www.mongodb.org/display/DOCS/Connections) at mongodb.org.</span><span class="sxs-lookup"><span data-stu-id="86e80-103">For more information about connection strings, see [Connections](http://www.mongodb.org/display/DOCS/Connections) at mongodb.org.</span></span>

<span data-ttu-id="86e80-104">**This URI contains your database user name and password.  Treat it as sensitive information and do not share it.**</span><span class="sxs-lookup"><span data-stu-id="86e80-104">**This URI contains your database user name and password.  Treat it as sensitive information and do not share it.**</span></span>

<span data-ttu-id="86e80-105">You can retrieve this URI in the Azure Portal using the following steps:</span><span class="sxs-lookup"><span data-stu-id="86e80-105">You can retrieve this URI in the Azure Portal using the following steps:</span></span>

1. <span data-ttu-id="86e80-106">Select **Add-ons**.</span><span class="sxs-lookup"><span data-stu-id="86e80-106">Select **Add-ons**.</span></span>  
   <span data-ttu-id="86e80-107">![AddonsButton][button-addons]</span><span class="sxs-lookup"><span data-stu-id="86e80-107">![AddonsButton][button-addons]</span></span>
2. <span data-ttu-id="86e80-108">Locate your MongoLab service in your add-on list.</span><span class="sxs-lookup"><span data-stu-id="86e80-108">Locate your MongoLab service in your add-on list.</span></span>  
   ![MongolabEntry][entry-mongolabaddon]
3. <span data-ttu-id="86e80-110">Cick the name of your add-on to reach the add-on page.</span><span class="sxs-lookup"><span data-stu-id="86e80-110">Cick the name of your add-on to reach the add-on page.</span></span>
4. <span data-ttu-id="86e80-111">Click **Connection Info**.</span><span class="sxs-lookup"><span data-stu-id="86e80-111">Click **Connection Info**.</span></span>  
   <span data-ttu-id="86e80-112">![ConnectionInfoButton][button-connectioninfo]</span><span class="sxs-lookup"><span data-stu-id="86e80-112">![ConnectionInfoButton][button-connectioninfo]</span></span>  
   <span data-ttu-id="86e80-113">Your MongoLab URI displays:</span><span class="sxs-lookup"><span data-stu-id="86e80-113">Your MongoLab URI displays:</span></span>  
   <span data-ttu-id="86e80-114">![ConnectionInfoScreen][screen-connectioninfo]</span><span class="sxs-lookup"><span data-stu-id="86e80-114">![ConnectionInfoScreen][screen-connectioninfo]</span></span>  
5. <span data-ttu-id="86e80-115">Click the clipboard button to the right of the MONGOLAB_URI value to copy the full value to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="86e80-115">Click the clipboard button to the right of the MONGOLAB_URI value to copy the full value to the clipboard.</span></span>

[entry-mongolabaddon]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-get-connectioninfo-mongolab/entry-mongolabaddon.png
[button-connectioninfo]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-get-connectioninfo-mongolab/button-connectioninfo.png
[screen-connectioninfo]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-get-connectioninfo-mongolab/dialog-mongolab_connectioninfo.png
[button-addons]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/howto-get-connectioninfo-mongolab/button-addons.png




