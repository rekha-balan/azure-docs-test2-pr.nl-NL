<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> <span data-ttu-id="92885-101">When making changes to the StorSimple Adapter for SharePoint RBS configuration, you must be logged on with a user account that belongs to the Domain Admins group.</span><span class="sxs-lookup"><span data-stu-id="92885-101">When making changes to the StorSimple Adapter for SharePoint RBS configuration, you must be logged on with a user account that belongs to the Domain Admins group.</span></span> <span data-ttu-id="92885-102">Additionally, you must access the configuration page from a browser running on the same host as Central Administration.</span><span class="sxs-lookup"><span data-stu-id="92885-102">Additionally, you must access the configuration page from a browser running on the same host as Central Administration.</span></span>
> 
> 

#### <a name="to-configure-rbs"></a><span data-ttu-id="92885-103">To configure RBS</span><span class="sxs-lookup"><span data-stu-id="92885-103">To configure RBS</span></span>
1. <span data-ttu-id="92885-104">Open the SharePoint Central Administration page, and browse to **System Settings**.</span><span class="sxs-lookup"><span data-stu-id="92885-104">Open the SharePoint Central Administration page, and browse to **System Settings**.</span></span> 
2. <span data-ttu-id="92885-105">In the **Azure StorSimple** section, click **Configure StorSimple Adapter**.</span><span class="sxs-lookup"><span data-stu-id="92885-105">In the **Azure StorSimple** section, click **Configure StorSimple Adapter**.</span></span>
   
    ![Configure the StorSimple Adapter](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. <span data-ttu-id="92885-107">On the **Configure StorSimple Adapter** page:</span><span class="sxs-lookup"><span data-stu-id="92885-107">On the **Configure StorSimple Adapter** page:</span></span>
   
   1. <span data-ttu-id="92885-108">Make sure that the **Enable editing path** check box is selected.</span><span class="sxs-lookup"><span data-stu-id="92885-108">Make sure that the **Enable editing path** check box is selected.</span></span>
   2. <span data-ttu-id="92885-109">In the text box, type the Universal Naming Convention (UNC) path of the BLOB store.</span><span class="sxs-lookup"><span data-stu-id="92885-109">In the text box, type the Universal Naming Convention (UNC) path of the BLOB store.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="92885-110">The BLOB store volume must be hosted on an iSCSI volume configured on the StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="92885-110">The BLOB store volume must be hosted on an iSCSI volume configured on the StorSimple device.</span></span>

   3. <span data-ttu-id="92885-111">Click the **Enable** button below each of the content databases that you want to configure for remote storage.</span><span class="sxs-lookup"><span data-stu-id="92885-111">Click the **Enable** button below each of the content databases that you want to configure for remote storage.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="92885-112">The BLOB store must be shared and reachable by all web front-end (WFE) servers, and the user account that is configured for the SharePoint server farm must have access to the share.</span><span class="sxs-lookup"><span data-stu-id="92885-112">The BLOB store must be shared and reachable by all web front-end (WFE) servers, and the user account that is configured for the SharePoint server farm must have access to the share.</span></span>
      
      ![Enable the RBS provider](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      <span data-ttu-id="92885-114">When you enable or disable RBS, you will also see the following message.</span><span class="sxs-lookup"><span data-stu-id="92885-114">When you enable or disable RBS, you will also see the following message.</span></span>
      
      ![Configure StorSimple Adapter Enable Disable](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. <span data-ttu-id="92885-116">Click the **Update** button to apply the configuration.</span><span class="sxs-lookup"><span data-stu-id="92885-116">Click the **Update** button to apply the configuration.</span></span> <span data-ttu-id="92885-117">When you click the **Update** button, the RBS configuration status will be updated on all WFE servers, and the entire farm will be RBS-enabled.</span><span class="sxs-lookup"><span data-stu-id="92885-117">When you click the **Update** button, the RBS configuration status will be updated on all WFE servers, and the entire farm will be RBS-enabled.</span></span> <span data-ttu-id="92885-118">The following message appears.</span><span class="sxs-lookup"><span data-stu-id="92885-118">The following message appears.</span></span>
      
      ![Adapter configuration message](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > <span data-ttu-id="92885-120">If you are configuring RBS for a SharePoint farm with a very large number of databases (greater than 200), the SharePoint Central Administration web page might time out. If that occurs, refresh the page.</span><span class="sxs-lookup"><span data-stu-id="92885-120">If you are configuring RBS for a SharePoint farm with a very large number of databases (greater than 200), the SharePoint Central Administration web page might time out. If that occurs, refresh the page.</span></span> <span data-ttu-id="92885-121">This does not affect the configuration process.</span><span class="sxs-lookup"><span data-stu-id="92885-121">This does not affect the configuration process.</span></span>

4. <span data-ttu-id="92885-122">Verify the configuration:</span><span class="sxs-lookup"><span data-stu-id="92885-122">Verify the configuration:</span></span>
   
   1. <span data-ttu-id="92885-123">Log on to the SharePoint Central Administration website, and browse to the **Configure StorSimple Adapter** page.</span><span class="sxs-lookup"><span data-stu-id="92885-123">Log on to the SharePoint Central Administration website, and browse to the **Configure StorSimple Adapter** page.</span></span>
   2. <span data-ttu-id="92885-124">Check the configuration details to make sure that they match the settings that you entered.</span><span class="sxs-lookup"><span data-stu-id="92885-124">Check the configuration details to make sure that they match the settings that you entered.</span></span> 
5. <span data-ttu-id="92885-125">Verify that RBS works correctly:</span><span class="sxs-lookup"><span data-stu-id="92885-125">Verify that RBS works correctly:</span></span>
   
   1. <span data-ttu-id="92885-126">Upload a document to SharePoint.</span><span class="sxs-lookup"><span data-stu-id="92885-126">Upload a document to SharePoint.</span></span> 
   2. <span data-ttu-id="92885-127">Browse to the UNC path that you configured.</span><span class="sxs-lookup"><span data-stu-id="92885-127">Browse to the UNC path that you configured.</span></span> <span data-ttu-id="92885-128">Make sure that the RBS directory structure was created and that it contains the uploaded object.</span><span class="sxs-lookup"><span data-stu-id="92885-128">Make sure that the RBS directory structure was created and that it contains the uploaded object.</span></span>
6. <span data-ttu-id="92885-129">(Optional) You can use the Microsoft RBS `Migrate()` PowerShell cmdlet included with SharePoint to migrate existing BLOB content to the StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="92885-129">(Optional) You can use the Microsoft RBS `Migrate()` PowerShell cmdlet included with SharePoint to migrate existing BLOB content to the StorSimple device.</span></span> <span data-ttu-id="92885-130">For more information, see [Migrate content into or out of RBS in SharePoint 2013][6] or [Migrate content into or out of RBS (SharePoint Foundation 2010)][7].</span><span class="sxs-lookup"><span data-stu-id="92885-130">For more information, see [Migrate content into or out of RBS in SharePoint 2013][6] or [Migrate content into or out of RBS (SharePoint Foundation 2010)][7].</span></span>
7. <span data-ttu-id="92885-131">(Optional) On test installations, you can verify that the BLOBs were moved out of the content database as follows:</span><span class="sxs-lookup"><span data-stu-id="92885-131">(Optional) On test installations, you can verify that the BLOBs were moved out of the content database as follows:</span></span> 
   
   1. <span data-ttu-id="92885-132">Start SQL Management Studio.</span><span class="sxs-lookup"><span data-stu-id="92885-132">Start SQL Management Studio.</span></span>
   2. <span data-ttu-id="92885-133">Run the ListBlobsInDB_2010.sql or ListBlobsInDB_2013.sql query, as follows.</span><span class="sxs-lookup"><span data-stu-id="92885-133">Run the ListBlobsInDB_2010.sql or ListBlobsInDB_2013.sql query, as follows.</span></span>
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      <span data-ttu-id="92885-134">If RBS was configured correctly, a NULL value should appear in the SizeOfContentInDB column for any object that was uploaded and successfully externalized with RBS.</span><span class="sxs-lookup"><span data-stu-id="92885-134">If RBS was configured correctly, a NULL value should appear in the SizeOfContentInDB column for any object that was uploaded and successfully externalized with RBS.</span></span>
8. <span data-ttu-id="92885-135">(Optional) After you configure RBS and move all BLOB content to the StorSimple device, you can move the content database to the device.</span><span class="sxs-lookup"><span data-stu-id="92885-135">(Optional) After you configure RBS and move all BLOB content to the StorSimple device, you can move the content database to the device.</span></span> <span data-ttu-id="92885-136">If you choose to move the content database, we recommend that you configure the content database storage on the device as a primary volume.</span><span class="sxs-lookup"><span data-stu-id="92885-136">If you choose to move the content database, we recommend that you configure the content database storage on the device as a primary volume.</span></span> <span data-ttu-id="92885-137">Then, use established SQL Server best practices to migrate the content database to the StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="92885-137">Then, use established SQL Server best practices to migrate the content database to the StorSimple device.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="92885-138">Moving the content database to the device is only supported for the StorSimple 8000 series (it is not supported for the 5000 or 7000 series).</span><span class="sxs-lookup"><span data-stu-id="92885-138">Moving the content database to the device is only supported for the StorSimple 8000 series (it is not supported for the 5000 or 7000 series).</span></span>
   
   <span data-ttu-id="92885-139">If you store BLOBs and the content database in separate volumes on the StorSimple device, we recommend that you configure them in the same volume container.</span><span class="sxs-lookup"><span data-stu-id="92885-139">If you store BLOBs and the content database in separate volumes on the StorSimple device, we recommend that you configure them in the same volume container.</span></span> <span data-ttu-id="92885-140">This ensures that they will be backed up together.</span><span class="sxs-lookup"><span data-stu-id="92885-140">This ensures that they will be backed up together.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="92885-141">If you have not enabled RBS, we do not recommend moving the content database to the StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="92885-141">If you have not enabled RBS, we do not recommend moving the content database to the StorSimple device.</span></span> <span data-ttu-id="92885-142">This is an untested configuration.</span><span class="sxs-lookup"><span data-stu-id="92885-142">This is an untested configuration.</span></span>
   
9. <span data-ttu-id="92885-143">Go to the next step: [Configure garbage collection](#configure-garbage-collection).</span><span class="sxs-lookup"><span data-stu-id="92885-143">Go to the next step: [Configure garbage collection](#configure-garbage-collection).</span></span>

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx




