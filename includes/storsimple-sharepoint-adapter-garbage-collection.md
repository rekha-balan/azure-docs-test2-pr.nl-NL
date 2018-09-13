<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="77fe3-101">In this procedure, you will:</span><span class="sxs-lookup"><span data-stu-id="77fe3-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="77fe3-102">[Prepare to run the Maintainer executable](#to-prepare-to-run-the-maintainer) .</span><span class="sxs-lookup"><span data-stu-id="77fe3-102">[Prepare to run the Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="77fe3-103">[Prepare the content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span><span class="sxs-lookup"><span data-stu-id="77fe3-103">[Prepare the content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="77fe3-104">[Run Maintainer.exe](#to-run-the-maintainer).</span><span class="sxs-lookup"><span data-stu-id="77fe3-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="77fe3-105">[Revert the content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span><span class="sxs-lookup"><span data-stu-id="77fe3-105">[Revert the content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="to-prepare-to-run-the-maintainer"></a><span data-ttu-id="77fe3-106">To prepare to run the Maintainer</span><span class="sxs-lookup"><span data-stu-id="77fe3-106">To prepare to run the Maintainer</span></span>
1. <span data-ttu-id="77fe3-107">On the Web front-end server, open the SharePoint 2013 Management Shell as an administrator.</span><span class="sxs-lookup"><span data-stu-id="77fe3-107">On the Web front-end server, open the SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="77fe3-108">Navigate to the folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span><span class="sxs-lookup"><span data-stu-id="77fe3-108">Navigate to the folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="77fe3-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** to **web.config**.</span><span class="sxs-lookup"><span data-stu-id="77fe3-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** to **web.config**.</span></span>
4. <span data-ttu-id="77fe3-110">Use `aspnet_regiis -pdf connectionStrings` to decrypt the web.config file.</span><span class="sxs-lookup"><span data-stu-id="77fe3-110">Use `aspnet_regiis -pdf connectionStrings` to decrypt the web.config file.</span></span>
5. <span data-ttu-id="77fe3-111">In the decrypted web.config file, under the `connectionStrings` node, add the connection string for your SQL server instance and the content database name.</span><span class="sxs-lookup"><span data-stu-id="77fe3-111">In the decrypted web.config file, under the `connectionStrings` node, add the connection string for your SQL server instance and the content database name.</span></span> <span data-ttu-id="77fe3-112">See the following example.</span><span class="sxs-lookup"><span data-stu-id="77fe3-112">See the following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="77fe3-113">Use `aspnet_regiis –pef connectionStrings` to re-encrypt the web.config file.</span><span class="sxs-lookup"><span data-stu-id="77fe3-113">Use `aspnet_regiis –pef connectionStrings` to re-encrypt the web.config file.</span></span> 
7. <span data-ttu-id="77fe3-114">Rename web.config to Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span><span class="sxs-lookup"><span data-stu-id="77fe3-114">Rename web.config to Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs"></a><span data-ttu-id="77fe3-115">To prepare the content database and Recycle Bin to immediately delete orphaned BLOBs</span><span class="sxs-lookup"><span data-stu-id="77fe3-115">To prepare the content database and Recycle Bin to immediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="77fe3-116">On the SQL Server, in SQL Management Studio, run the following update queries for the target content database:</span><span class="sxs-lookup"><span data-stu-id="77fe3-116">On the SQL Server, in SQL Management Studio, run the following update queries for the target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="77fe3-117">On the web front-end server, under **Central Administration**, edit the **Web Application General Settings** for the desired content database to temporarily disable the Recycle Bin.</span><span class="sxs-lookup"><span data-stu-id="77fe3-117">On the web front-end server, under **Central Administration**, edit the **Web Application General Settings** for the desired content database to temporarily disable the Recycle Bin.</span></span> <span data-ttu-id="77fe3-118">This action will also empty the Recycle Bin for any related site collections.</span><span class="sxs-lookup"><span data-stu-id="77fe3-118">This action will also empty the Recycle Bin for any related site collections.</span></span> <span data-ttu-id="77fe3-119">To do this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span><span class="sxs-lookup"><span data-stu-id="77fe3-119">To do this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="77fe3-120">Set the **Recycle Bin Status** to **OFF**.</span><span class="sxs-lookup"><span data-stu-id="77fe3-120">Set the **Recycle Bin Status** to **OFF**.</span></span>
   
    ![Web Application General Settings](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="to-run-the-maintainer"></a><span data-ttu-id="77fe3-122">To run the Maintainer</span><span class="sxs-lookup"><span data-stu-id="77fe3-122">To run the Maintainer</span></span>
* <span data-ttu-id="77fe3-123">On the web front-end server, in the SharePoint 2013 Management Shell, run the Maintainer as follows:</span><span class="sxs-lookup"><span data-stu-id="77fe3-123">On the web front-end server, in the SharePoint 2013 Management Shell, run the Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="77fe3-124">Only the `GarbageCollection` operation is supported for StorSimple at this time.</span><span class="sxs-lookup"><span data-stu-id="77fe3-124">Only the `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="77fe3-125">Also note that the parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span><span class="sxs-lookup"><span data-stu-id="77fe3-125">Also note that the parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="to-revert-the-content-database-and-recycle-bin-settings"></a><span data-ttu-id="77fe3-126">To revert the content database and Recycle Bin settings</span><span class="sxs-lookup"><span data-stu-id="77fe3-126">To revert the content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="77fe3-127">On the SQL Server, in SQL Management Studio, run the following update queries for the target content database:</span><span class="sxs-lookup"><span data-stu-id="77fe3-127">On the SQL Server, in SQL Management Studio, run the following update queries for the target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="77fe3-128">On the web front-end server, in **Central Administration**, edit the **Web Application General Settings** for the desired content database to re-enable the Recycle Bin.</span><span class="sxs-lookup"><span data-stu-id="77fe3-128">On the web front-end server, in **Central Administration**, edit the **Web Application General Settings** for the desired content database to re-enable the Recycle Bin.</span></span> <span data-ttu-id="77fe3-129">To do this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span><span class="sxs-lookup"><span data-stu-id="77fe3-129">To do this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="77fe3-130">Set the Recycle Bin Status to **ON**.</span><span class="sxs-lookup"><span data-stu-id="77fe3-130">Set the Recycle Bin Status to **ON**.</span></span>


