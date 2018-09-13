---
title: How to use Notification Hubs with Java
description: Learn how to use Azure Notification Hubs from a Java back-end.
services: notification-hubs
documentationcenter: ''
author: ysxu
manager: erikre
editor: ''
ms.assetid: 4c3f966d-0158-4a48-b949-9fa3666cb7e4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: java
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 41f978750ddef9f7e878c65b0017e909720154aa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660842"
---
# <a name="how-to-use-notification-hubs-from-java"></a><span data-ttu-id="36b9c-103">How to use Notification Hubs from Java</span><span class="sxs-lookup"><span data-stu-id="36b9c-103">How to use Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="36b9c-104">This topic describes the key features of the new fully supported official Azure Notification Hub Java SDK.</span><span class="sxs-lookup"><span data-stu-id="36b9c-104">This topic describes the key features of the new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="36b9c-105">This is an open source project and you can view the entire SDK code at [Java SDK].</span><span class="sxs-lookup"><span data-stu-id="36b9c-105">This is an open source project and you can view the entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="36b9c-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="36b9c-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="36b9c-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span><span class="sxs-lookup"><span data-stu-id="36b9c-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="36b9c-108">The SDK supports currently:</span><span class="sxs-lookup"><span data-stu-id="36b9c-108">The SDK supports currently:</span></span>

* <span data-ttu-id="36b9c-109">CRUD on Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="36b9c-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="36b9c-110">CRUD on Registrations</span><span class="sxs-lookup"><span data-stu-id="36b9c-110">CRUD on Registrations</span></span>
* <span data-ttu-id="36b9c-111">Installation Management</span><span class="sxs-lookup"><span data-stu-id="36b9c-111">Installation Management</span></span>
* <span data-ttu-id="36b9c-112">Import/Export Registrations</span><span class="sxs-lookup"><span data-stu-id="36b9c-112">Import/Export Registrations</span></span>
* <span data-ttu-id="36b9c-113">Regular Sends</span><span class="sxs-lookup"><span data-stu-id="36b9c-113">Regular Sends</span></span>
* <span data-ttu-id="36b9c-114">Scheduled Sends</span><span class="sxs-lookup"><span data-stu-id="36b9c-114">Scheduled Sends</span></span>
* <span data-ttu-id="36b9c-115">Async operations via Java NIO</span><span class="sxs-lookup"><span data-stu-id="36b9c-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="36b9c-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span><span class="sxs-lookup"><span data-stu-id="36b9c-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="36b9c-117">SDK Usage</span><span class="sxs-lookup"><span data-stu-id="36b9c-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="36b9c-118">Compile and build</span><span class="sxs-lookup"><span data-stu-id="36b9c-118">Compile and build</span></span>
<span data-ttu-id="36b9c-119">Use [Maven]</span><span class="sxs-lookup"><span data-stu-id="36b9c-119">Use [Maven]</span></span>

<span data-ttu-id="36b9c-120">To build:</span><span class="sxs-lookup"><span data-stu-id="36b9c-120">To build:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="36b9c-121">Code</span><span class="sxs-lookup"><span data-stu-id="36b9c-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="36b9c-122">Notification Hub CRUDs</span><span class="sxs-lookup"><span data-stu-id="36b9c-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="36b9c-123">**Create a NamespaceManager:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="36b9c-124">**Create Notification Hub:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="36b9c-125">OR</span><span class="sxs-lookup"><span data-stu-id="36b9c-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="36b9c-126">**Get Notification Hub:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="36b9c-127">**Update Notification Hub:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="36b9c-128">**Delete Notification Hub:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="36b9c-129">Registration CRUDs</span><span class="sxs-lookup"><span data-stu-id="36b9c-129">Registration CRUDs</span></span>
<span data-ttu-id="36b9c-130">**Create a Notification Hub client:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="36b9c-131">**Create Windows registration:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="36b9c-132">**Create iOS registration:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="36b9c-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span><span class="sxs-lookup"><span data-stu-id="36b9c-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="36b9c-134">**Create template registrations:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="36b9c-135">**Create registrations using create registrationid + upsert pattern**</span><span class="sxs-lookup"><span data-stu-id="36b9c-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="36b9c-136">Removes duplicates due to any lost responses if storing registration ids on the device:</span><span class="sxs-lookup"><span data-stu-id="36b9c-136">Removes duplicates due to any lost responses if storing registration ids on the device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="36b9c-137">**Update registrations:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="36b9c-138">**Delete registrations:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="36b9c-139">**Query registrations:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-139">**Query registrations:**</span></span>

* <span data-ttu-id="36b9c-140">**Get single registration:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="36b9c-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="36b9c-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="36b9c-142">**Get all registrations in hub:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="36b9c-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="36b9c-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="36b9c-144">**Get registrations with tag:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="36b9c-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="36b9c-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="36b9c-146">**Get registrations by channel:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="36b9c-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="36b9c-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="36b9c-148">All collection queries support $top and continuation tokens.</span><span class="sxs-lookup"><span data-stu-id="36b9c-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="36b9c-149">Installation API usage</span><span class="sxs-lookup"><span data-stu-id="36b9c-149">Installation API usage</span></span>
<span data-ttu-id="36b9c-150">Installation API is an alternative mechanism for registration management.</span><span class="sxs-lookup"><span data-stu-id="36b9c-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="36b9c-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible to use a SINGLE Installation object.</span><span class="sxs-lookup"><span data-stu-id="36b9c-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible to use a SINGLE Installation object.</span></span> <span data-ttu-id="36b9c-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span><span class="sxs-lookup"><span data-stu-id="36b9c-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="36b9c-153">You don't need to call the service to get Id anymore - just generate GUID or any other identifier, keep it on device and send to your backend together with push channel (device token).</span><span class="sxs-lookup"><span data-stu-id="36b9c-153">You don't need to call the service to get Id anymore - just generate GUID or any other identifier, keep it on device and send to your backend together with push channel (device token).</span></span> <span data-ttu-id="36b9c-154">On the backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free to retry if needed.</span><span class="sxs-lookup"><span data-stu-id="36b9c-154">On the backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free to retry if needed.</span></span>

<span data-ttu-id="36b9c-155">As example for Amazon Kindle Fire it looks like this:</span><span class="sxs-lookup"><span data-stu-id="36b9c-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="36b9c-156">If you want to update it:</span><span class="sxs-lookup"><span data-stu-id="36b9c-156">If you want to update it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="36b9c-157">For advanced scenarios we have partial update capability which allows to modify only particular properties of the installation object.</span><span class="sxs-lookup"><span data-stu-id="36b9c-157">For advanced scenarios we have partial update capability which allows to modify only particular properties of the installation object.</span></span> <span data-ttu-id="36b9c-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span><span class="sxs-lookup"><span data-stu-id="36b9c-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="36b9c-159">Delete Installation:</span><span class="sxs-lookup"><span data-stu-id="36b9c-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="36b9c-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span><span class="sxs-lookup"><span data-stu-id="36b9c-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="36b9c-161">Your requested operation just goes to the system queue during the call and will be executed in background.</span><span class="sxs-lookup"><span data-stu-id="36b9c-161">Your requested operation just goes to the system queue during the call and will be executed in background.</span></span> <span data-ttu-id="36b9c-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by the service.</span><span class="sxs-lookup"><span data-stu-id="36b9c-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by the service.</span></span>

<span data-ttu-id="36b9c-163">Send flow for Installations is the same as for Registrations.</span><span class="sxs-lookup"><span data-stu-id="36b9c-163">Send flow for Installations is the same as for Registrations.</span></span> <span data-ttu-id="36b9c-164">We've just introduced an option to target notification to the particular Installation - just use tag "InstallationId:{desired-id}".</span><span class="sxs-lookup"><span data-stu-id="36b9c-164">We've just introduced an option to target notification to the particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="36b9c-165">For case above it would look like this:</span><span class="sxs-lookup"><span data-stu-id="36b9c-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="36b9c-166">For one of several templates:</span><span class="sxs-lookup"><span data-stu-id="36b9c-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="36b9c-167">Schedule Notifications (available for STANDARD Tier)</span><span class="sxs-lookup"><span data-stu-id="36b9c-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="36b9c-168">The same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span><span class="sxs-lookup"><span data-stu-id="36b9c-168">The same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="36b9c-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span><span class="sxs-lookup"><span data-stu-id="36b9c-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="36b9c-170">**Schedule a Windows native notification:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="36b9c-171">Import/Export (available for STANDARD Tier)</span><span class="sxs-lookup"><span data-stu-id="36b9c-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="36b9c-172">Sometimes it is required to perform bulk operation against registrations.</span><span class="sxs-lookup"><span data-stu-id="36b9c-172">Sometimes it is required to perform bulk operation against registrations.</span></span> <span data-ttu-id="36b9c-173">Usually it is for integration with another system or just a massive fix to say update the tags.</span><span class="sxs-lookup"><span data-stu-id="36b9c-173">Usually it is for integration with another system or just a massive fix to say update the tags.</span></span> <span data-ttu-id="36b9c-174">It is strongly not recommended to use Get/Update flow if we are talking about thousands of registrations.</span><span class="sxs-lookup"><span data-stu-id="36b9c-174">It is strongly not recommended to use Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="36b9c-175">Import/Export capability is designed to cover the scenario.</span><span class="sxs-lookup"><span data-stu-id="36b9c-175">Import/Export capability is designed to cover the scenario.</span></span> <span data-ttu-id="36b9c-176">Basically you provide an access to some blob container under your storage account as a source of incoming data and location for output.</span><span class="sxs-lookup"><span data-stu-id="36b9c-176">Basically you provide an access to some blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="36b9c-177">**Submit export job:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="36b9c-178">**Submit import job:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="36b9c-179">**Wait until job is done:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="36b9c-180">**Get all jobs:**</span><span class="sxs-lookup"><span data-stu-id="36b9c-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="36b9c-181">**URI with SAS signature:** This is the URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span><span class="sxs-lookup"><span data-stu-id="36b9c-181">**URI with SAS signature:** This is the URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="36b9c-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span><span class="sxs-lookup"><span data-stu-id="36b9c-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="36b9c-183">As simple alternative you can take a look at ImportExportE2E test class (from the github location) which has very basic and compact implementation of signing algorithm.</span><span class="sxs-lookup"><span data-stu-id="36b9c-183">As simple alternative you can take a look at ImportExportE2E test class (from the github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="36b9c-184">Send Notifications</span><span class="sxs-lookup"><span data-stu-id="36b9c-184">Send Notifications</span></span>
<span data-ttu-id="36b9c-185">The Notification object is simply a body with headers, some utility methods help in building the native and template notifications objects.</span><span class="sxs-lookup"><span data-stu-id="36b9c-185">The Notification object is simply a body with headers, some utility methods help in building the native and template notifications objects.</span></span>

* <span data-ttu-id="36b9c-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span><span class="sxs-lookup"><span data-stu-id="36b9c-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="36b9c-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="36b9c-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="36b9c-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="36b9c-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="36b9c-189">**Windows Phone 8.0 and 8.1 Silverlight**</span><span class="sxs-lookup"><span data-stu-id="36b9c-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="36b9c-190">**Kindle Fire**</span><span class="sxs-lookup"><span data-stu-id="36b9c-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="36b9c-191">**Send to Tags**</span><span class="sxs-lookup"><span data-stu-id="36b9c-191">**Send to Tags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="36b9c-192">**Send to tag expression**</span><span class="sxs-lookup"><span data-stu-id="36b9c-192">**Send to tag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="36b9c-193">**Send template notification**</span><span class="sxs-lookup"><span data-stu-id="36b9c-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="36b9c-194">Running your Java code should now produce a notification appearing on your target device.</span><span class="sxs-lookup"><span data-stu-id="36b9c-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36b9c-195">Next Steps</span><span class="sxs-lookup"><span data-stu-id="36b9c-195">Next Steps</span></span>
<span data-ttu-id="36b9c-196">In this topic we showed how to create a simple Java REST client for Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="36b9c-196">In this topic we showed how to create a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="36b9c-197">From here you can:</span><span class="sxs-lookup"><span data-stu-id="36b9c-197">From here you can:</span></span>

* <span data-ttu-id="36b9c-198">Download the full [Java SDK], which contains the entire SDK code.</span><span class="sxs-lookup"><span data-stu-id="36b9c-198">Download the full [Java SDK], which contains the entire SDK code.</span></span> 
* <span data-ttu-id="36b9c-199">Play with the samples:</span><span class="sxs-lookup"><span data-stu-id="36b9c-199">Play with the samples:</span></span>
  * <span data-ttu-id="36b9c-200">[Get Started with Notification Hubs]</span><span class="sxs-lookup"><span data-stu-id="36b9c-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="36b9c-201">[Send breaking news]</span><span class="sxs-lookup"><span data-stu-id="36b9c-201">[Send breaking news]</span></span>
  * <span data-ttu-id="36b9c-202">[Send localized breaking news]</span><span class="sxs-lookup"><span data-stu-id="36b9c-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="36b9c-203">[Send notifications to authenticated users]</span><span class="sxs-lookup"><span data-stu-id="36b9c-203">[Send notifications to authenticated users]</span></span>
  * <span data-ttu-id="36b9c-204">[Send cross-platform notifications to authenticated users]</span><span class="sxs-lookup"><span data-stu-id="36b9c-204">[Send cross-platform notifications to authenticated users]</span></span>

[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Get Started with Notification Hubs]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[Send breaking news]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[Send localized breaking news]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Send notifications to authenticated users]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Send cross-platform notifications to authenticated users]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

