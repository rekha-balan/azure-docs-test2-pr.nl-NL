---
title: How to use the Azure Mobile Apps SDK for Android | Microsoft Docs
description: How to use the Azure Mobile Apps SDK for Android
services: app-service\mobile
documentationcenter: android
author: conceptdev
manager: crdun
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 11/16/2017
ms.author: crdun
ms.openlocfilehash: 1ab7aa9ecdd51809f6e1d82958f21b78b16e7e63
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809782"
---
# <a name="how-to-use-the-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="d9ce8-103">How to use the Azure Mobile Apps SDK for Android</span><span class="sxs-lookup"><span data-stu-id="d9ce8-103">How to use the Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="d9ce8-104">This guide shows you how to use the Android client SDK for Mobile Apps to implement common scenarios, such as:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-104">This guide shows you how to use the Android client SDK for Mobile Apps to implement common scenarios, such as:</span></span>

* <span data-ttu-id="d9ce8-105">Querying for data (inserting, updating, and deleting).</span><span class="sxs-lookup"><span data-stu-id="d9ce8-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="d9ce8-106">Authentication.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-106">Authentication.</span></span>
* <span data-ttu-id="d9ce8-107">Handling errors.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-107">Handling errors.</span></span>
* <span data-ttu-id="d9ce8-108">Customizing the client.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-108">Customizing the client.</span></span>

<span data-ttu-id="d9ce8-109">This guide focuses on the client-side Android SDK.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-109">This guide focuses on the client-side Android SDK.</span></span>  <span data-ttu-id="d9ce8-110">To learn more about the server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How to use the Node.js backend SDK][11].</span><span class="sxs-lookup"><span data-stu-id="d9ce8-110">To learn more about the server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How to use the Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="d9ce8-111">Reference Documentation</span><span class="sxs-lookup"><span data-stu-id="d9ce8-111">Reference Documentation</span></span>

<span data-ttu-id="d9ce8-112">You can find the [Javadocs API reference][12] for the Android client library on GitHub.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-112">You can find the [Javadocs API reference][12] for the Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="d9ce8-113">Supported Platforms</span><span class="sxs-lookup"><span data-stu-id="d9ce8-113">Supported Platforms</span></span>

<span data-ttu-id="d9ce8-114">The Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-114">The Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="d9ce8-115">Authentication, in particular, utilizes a common web framework approach to gather credentials.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-115">Authentication, in particular, utilizes a common web framework approach to gather credentials.</span></span>  <span data-ttu-id="d9ce8-116">Server-flow authentication does not work with small form factor devices such as watches.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="d9ce8-117">Setup and Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d9ce8-117">Setup and Prerequisites</span></span>

<span data-ttu-id="d9ce8-118">Complete the [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-118">Complete the [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="d9ce8-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="d9ce8-120">The Quickstart also helps you configure your account and create your first Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-120">The Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="d9ce8-121">If you decide not to complete the Quickstart tutorial, complete the following tasks:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-121">If you decide not to complete the Quickstart tutorial, complete the following tasks:</span></span>

* <span data-ttu-id="d9ce8-122">[create a Mobile App backend][13] to use with your Android app.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-122">[create a Mobile App backend][13] to use with your Android app.</span></span>
* <span data-ttu-id="d9ce8-123">In Android Studio, [update the Gradle build files](#gradle-build).</span><span class="sxs-lookup"><span data-stu-id="d9ce8-123">In Android Studio, [update the Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="d9ce8-124">[Enable internet permission](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="d9ce8-124">[Enable internet permission](#enable-internet).</span></span>

### <a name="gradle-build"></a><span data-ttu-id="d9ce8-125">Update the Gradle build file</span><span class="sxs-lookup"><span data-stu-id="d9ce8-125">Update the Gradle build file</span></span>

<span data-ttu-id="d9ce8-126">Change both **build.gradle** files:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="d9ce8-127">Add this code to the *Project* level **build.gradle** file inside the *buildscript* tag:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-127">Add this code to the *Project* level **build.gradle** file inside the *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="d9ce8-128">Add this code to the *Module app* level **build.gradle** file inside the *dependencies* tag:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-128">Add this code to the *Module app* level **build.gradle** file inside the *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.4.0@aar'
    ```

    <span data-ttu-id="d9ce8-129">Currently the latest version is 3.4.0.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-129">Currently the latest version is 3.4.0.</span></span> <span data-ttu-id="d9ce8-130">The supported versions are listed [on bintray][14].</span><span class="sxs-lookup"><span data-stu-id="d9ce8-130">The supported versions are listed [on bintray][14].</span></span>

### <a name="enable-internet"></a><span data-ttu-id="d9ce8-131">Enable internet permission</span><span class="sxs-lookup"><span data-stu-id="d9ce8-131">Enable internet permission</span></span>

<span data-ttu-id="d9ce8-132">To access Azure, your app must have the INTERNET permission enabled.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-132">To access Azure, your app must have the INTERNET permission enabled.</span></span> <span data-ttu-id="d9ce8-133">If it's not already enabled, add the following line of code to your **AndroidManifest.xml** file:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-133">If it's not already enabled, add the following line of code to your **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="d9ce8-134">Create a Client Connection</span><span class="sxs-lookup"><span data-stu-id="d9ce8-134">Create a Client Connection</span></span>

<span data-ttu-id="d9ce8-135">Azure Mobile Apps provides four functions to your mobile application:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-135">Azure Mobile Apps provides four functions to your mobile application:</span></span>

* <span data-ttu-id="d9ce8-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="d9ce8-137">Call Custom APIs written with the Azure Mobile Apps Server SDK.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-137">Call Custom APIs written with the Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="d9ce8-138">Authentication with Azure App Service Authentication and Authorization.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="d9ce8-139">Push Notification Registration with Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="d9ce8-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="d9ce8-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span><span class="sxs-lookup"><span data-stu-id="d9ce8-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="d9ce8-142">To create a `MobileServiceClient` object:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-142">To create a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with the Site URL
    this);                  // Your application Context
```

<span data-ttu-id="d9ce8-143">The `<MobileAppUrl>` is either a string or a URL object that points to your mobile backend.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-143">The `<MobileAppUrl>` is either a string or a URL object that points to your mobile backend.</span></span>  <span data-ttu-id="d9ce8-144">If you are using Azure App Service to host your mobile backend, then ensure you use the secure `https://` version of the URL.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-144">If you are using Azure App Service to host your mobile backend, then ensure you use the secure `https://` version of the URL.</span></span>

<span data-ttu-id="d9ce8-145">The client also requires access to the Activity or Context - the `this` parameter in the example.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-145">The client also requires access to the Activity or Context - the `this` parameter in the example.</span></span>  <span data-ttu-id="d9ce8-146">The MobileServiceClient construction should happen within the `onCreate()` method of the Activity referenced in the `AndroidManifest.xml` file.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-146">The MobileServiceClient construction should happen within the `onCreate()` method of the Activity referenced in the `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="d9ce8-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="d9ce8-148">In this case, you should pass the Activity within the constructor to appropriately configure the service.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-148">In this case, you should pass the Activity within the constructor to appropriately configure the service.</span></span>  <span data-ttu-id="d9ce8-149">For example:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-149">For example:</span></span>

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public class AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

<span data-ttu-id="d9ce8-150">You can now call `AzureServiceAdapter.Initialize(this);` in the `onCreate()` method of your main activity.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-150">You can now call `AzureServiceAdapter.Initialize(this);` in the `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="d9ce8-151">Any other methods needing access to the client use `AzureServiceAdapter.getInstance();` to obtain a reference to the service adapter.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-151">Any other methods needing access to the client use `AzureServiceAdapter.getInstance();` to obtain a reference to the service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="d9ce8-152">Data Operations</span><span class="sxs-lookup"><span data-stu-id="d9ce8-152">Data Operations</span></span>

<span data-ttu-id="d9ce8-153">The core of the Azure Mobile Apps SDK is to provide access to data stored within SQL Azure on the Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-153">The core of the Azure Mobile Apps SDK is to provide access to data stored within SQL Azure on the Mobile App backend.</span></span>  <span data-ttu-id="d9ce8-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span><span class="sxs-lookup"><span data-stu-id="d9ce8-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="d9ce8-155">The bulk of this section deals with using strongly typed classes.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-155">The bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="d9ce8-156">Define client data classes</span><span class="sxs-lookup"><span data-stu-id="d9ce8-156">Define client data classes</span></span>

<span data-ttu-id="d9ce8-157">To access data from SQL Azure tables, define client data classes that correspond to the tables in the Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-157">To access data from SQL Azure tables, define client data classes that correspond to the tables in the Mobile App backend.</span></span> <span data-ttu-id="d9ce8-158">Examples in this topic assume a table named **MyDataTable**, which has the following columns:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-158">Examples in this topic assume a table named **MyDataTable**, which has the following columns:</span></span>

* <span data-ttu-id="d9ce8-159">id</span><span class="sxs-lookup"><span data-stu-id="d9ce8-159">id</span></span>
* <span data-ttu-id="d9ce8-160">text</span><span class="sxs-lookup"><span data-stu-id="d9ce8-160">text</span></span>
* <span data-ttu-id="d9ce8-161">complete</span><span class="sxs-lookup"><span data-stu-id="d9ce8-161">complete</span></span>

<span data-ttu-id="d9ce8-162">The corresponding typed client-side object resides in a file called **MyDataTable.java**:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-162">The corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="d9ce8-163">Add getter and setter methods for each field that you add.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="d9ce8-164">If your SQL Azure table contains more columns, you would add the corresponding fields to this class.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-164">If your SQL Azure table contains more columns, you would add the corresponding fields to this class.</span></span>  <span data-ttu-id="d9ce8-165">For example, if the DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-165">For example, if the DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns the item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets the item priority
*
* @param priority
*            priority to set
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="d9ce8-166">To learn how to create additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span><span class="sxs-lookup"><span data-stu-id="d9ce8-166">To learn how to create additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="d9ce8-167">An Azure Mobile Apps backend table defines five special fields, four of which are available to clients:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-167">An Azure Mobile Apps backend table defines five special fields, four of which are available to clients:</span></span>

* <span data-ttu-id="d9ce8-168">`String id`: The globally unique ID for the record.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-168">`String id`: The globally unique ID for the record.</span></span>  <span data-ttu-id="d9ce8-169">As a best practice, make the id the String representation of a [UUID][17] object.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-169">As a best practice, make the id the String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="d9ce8-170">`DateTimeOffset updatedAt`: The date/time of the last update.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-170">`DateTimeOffset updatedAt`: The date/time of the last update.</span></span>  <span data-ttu-id="d9ce8-171">The updatedAt field is set by the server and should never be set by your client code.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-171">The updatedAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="d9ce8-172">`DateTimeOffset createdAt`: The date/time that the object was created.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-172">`DateTimeOffset createdAt`: The date/time that the object was created.</span></span>  <span data-ttu-id="d9ce8-173">The createdAt field is set by the server and should never be set by your client code.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-173">The createdAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="d9ce8-174">`byte[] version`: Normally represented as a string, the version is also set by the server.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-174">`byte[] version`: Normally represented as a string, the version is also set by the server.</span></span>
* <span data-ttu-id="d9ce8-175">`boolean deleted`: Indicates that the record has been deleted but not purged yet.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-175">`boolean deleted`: Indicates that the record has been deleted but not purged yet.</span></span>  <span data-ttu-id="d9ce8-176">Do not use `deleted` as a property in your class.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="d9ce8-177">The `id` field is required.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-177">The `id` field is required.</span></span>  <span data-ttu-id="d9ce8-178">The `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span><span class="sxs-lookup"><span data-stu-id="d9ce8-178">The `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="d9ce8-179">The `createdAt` field is a reference field and is not used by the client.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-179">The `createdAt` field is a reference field and is not used by the client.</span></span>  <span data-ttu-id="d9ce8-180">The names are "across-the-wire" names of the properties and are not adjustable.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-180">The names are "across-the-wire" names of the properties and are not adjustable.</span></span>  <span data-ttu-id="d9ce8-181">However, you can create a mapping between your object and the "across-the-wire" names using the [gson][3] library.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-181">However, you can create a mapping between your object and the "across-the-wire" names using the [gson][3] library.</span></span>  <span data-ttu-id="d9ce8-182">For example:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-182">For example:</span></span>

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getCreatedAt() { return mCreatedAt; }
    protected void setCreatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected void setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getVersion() { return mVersion; }
    public final void setVersion(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a><span data-ttu-id="d9ce8-183">Create a Table Reference</span><span class="sxs-lookup"><span data-stu-id="d9ce8-183">Create a Table Reference</span></span>

<span data-ttu-id="d9ce8-184">To access a table, first create a [MobileServiceTable][8] object by calling the **getTable** method on the [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="d9ce8-184">To access a table, first create a [MobileServiceTable][8] object by calling the **getTable** method on the [MobileServiceClient][9].</span></span>  <span data-ttu-id="d9ce8-185">This method has two overloads:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="d9ce8-186">In the following code, **mClient** is a reference to your MobileServiceClient object.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-186">In the following code, **mClient** is a reference to your MobileServiceClient object.</span></span>  <span data-ttu-id="d9ce8-187">The first overload is used where the class name and the table name are the same, and is the one used in the Quickstart:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-187">The first overload is used where the class name and the table name are the same, and is the one used in the Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="d9ce8-188">The second overload is used when the table name is different from the class name: the first parameter is the table name.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-188">The second overload is used when the table name is different from the class name: the first parameter is the table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <a name="query"></a><span data-ttu-id="d9ce8-189">Query a Backend Table</span><span class="sxs-lookup"><span data-stu-id="d9ce8-189">Query a Backend Table</span></span>

<span data-ttu-id="d9ce8-190">First, obtain a table reference.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-190">First, obtain a table reference.</span></span>  <span data-ttu-id="d9ce8-191">Then execute a query on the table reference.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-191">Then execute a query on the table reference.</span></span>  <span data-ttu-id="d9ce8-192">A query is any combination of:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-192">A query is any combination of:</span></span>

* <span data-ttu-id="d9ce8-193">A `.where()` [filter clause](#filtering).</span><span class="sxs-lookup"><span data-stu-id="d9ce8-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="d9ce8-194">An `.orderBy()` [ordering clause](#sorting).</span><span class="sxs-lookup"><span data-stu-id="d9ce8-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="d9ce8-195">A `.select()` [field selection clause](#selection).</span><span class="sxs-lookup"><span data-stu-id="d9ce8-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="d9ce8-196">A `.skip()` and `.top()` for [paged results](#paging).</span><span class="sxs-lookup"><span data-stu-id="d9ce8-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="d9ce8-197">The clauses must be presented in the preceding order.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-197">The clauses must be presented in the preceding order.</span></span>

### <a name="filter"></a> <span data-ttu-id="d9ce8-198">Filtering Results</span><span class="sxs-lookup"><span data-stu-id="d9ce8-198">Filtering Results</span></span>

<span data-ttu-id="d9ce8-199">The general form of a query is:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-199">The general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts the async into a sync result
```

<span data-ttu-id="d9ce8-200">The preceding example returns all results (up to the maximum page size set by the server).</span><span class="sxs-lookup"><span data-stu-id="d9ce8-200">The preceding example returns all results (up to the maximum page size set by the server).</span></span>  <span data-ttu-id="d9ce8-201">The `.execute()` method executes the query on the backend.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-201">The `.execute()` method executes the query on the backend.</span></span>  <span data-ttu-id="d9ce8-202">The query is converted to an [OData v3][19] query before transmission to the Mobile Apps backend.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-202">The query is converted to an [OData v3][19] query before transmission to the Mobile Apps backend.</span></span>  <span data-ttu-id="d9ce8-203">On receipt, the Mobile Apps backend converts the query into an SQL statement before executing it on the SQL Azure instance.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-203">On receipt, the Mobile Apps backend converts the query into an SQL statement before executing it on the SQL Azure instance.</span></span>  <span data-ttu-id="d9ce8-204">Since network activity takes some time, The `.execute()` method returns a [`ListenableFuture<E>`][18].</span><span class="sxs-lookup"><span data-stu-id="d9ce8-204">Since network activity takes some time, The `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <a name="filtering"></a><span data-ttu-id="d9ce8-205">Filter returned data</span><span class="sxs-lookup"><span data-stu-id="d9ce8-205">Filter returned data</span></span>

<span data-ttu-id="d9ce8-206">The following query execution returns all items from the **ToDoItem** table where **complete** equals **false**.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-206">The following query execution returns all items from the **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="d9ce8-207">**mToDoTable** is the reference to the mobile service table that we created previously.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-207">**mToDoTable** is the reference to the mobile service table that we created previously.</span></span>

<span data-ttu-id="d9ce8-208">Define a filter using the **where** method call on the table reference.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-208">Define a filter using the **where** method call on the table reference.</span></span> <span data-ttu-id="d9ce8-209">The **where** method is followed by a **field** method followed by a method that specifies the logical predicate.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-209">The **where** method is followed by a **field** method followed by a method that specifies the logical predicate.</span></span> <span data-ttu-id="d9ce8-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span><span class="sxs-lookup"><span data-stu-id="d9ce8-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="d9ce8-211">These methods let you compare number and string fields to specific values.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-211">These methods let you compare number and string fields to specific values.</span></span>

<span data-ttu-id="d9ce8-212">You can filter on dates.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-212">You can filter on dates.</span></span> <span data-ttu-id="d9ce8-213">The following methods let you compare the entire date field or parts of the date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-213">The following methods let you compare the entire date field or parts of the date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="d9ce8-214">The following example adds a filter for items whose *due date* equals 2013.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-214">The following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="d9ce8-215">The following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-215">The following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="d9ce8-216">The following example filters for table rows where the *text* column starts with "PRI0."</span><span class="sxs-lookup"><span data-stu-id="d9ce8-216">The following example filters for table rows where the *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="d9ce8-217">The following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-217">The following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="d9ce8-218">The following example filters for table rows where the **duration** is an even number.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-218">The following example filters for table rows where the **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="d9ce8-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="d9ce8-220">The following example combines two of the preceding examples.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-220">The following example combines two of the preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="d9ce8-221">Group and nest logical operators:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-221">Group and nest logical operators:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

<span data-ttu-id="d9ce8-222">For more detailed discussion and examples of filtering, see [Exploring the richness of the Android client query model][20].</span><span class="sxs-lookup"><span data-stu-id="d9ce8-222">For more detailed discussion and examples of filtering, see [Exploring the richness of the Android client query model][20].</span></span>

### <a name="sorting"></a><span data-ttu-id="d9ce8-223">Sort returned data</span><span class="sxs-lookup"><span data-stu-id="d9ce8-223">Sort returned data</span></span>

<span data-ttu-id="d9ce8-224">The following code returns all items from a table of **ToDoItems** sorted ascending by the *text* field.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-224">The following code returns all items from a table of **ToDoItems** sorted ascending by the *text* field.</span></span> <span data-ttu-id="d9ce8-225">*mToDoTable* is the reference to the backend table that you created previously:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-225">*mToDoTable* is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="d9ce8-226">The first parameter of the **orderBy** method is a string equal to the name of the field on which to sort.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-226">The first parameter of the **orderBy** method is a string equal to the name of the field on which to sort.</span></span> <span data-ttu-id="d9ce8-227">The second parameter uses the **QueryOrder** enumeration to specify whether to sort ascending or descending.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-227">The second parameter uses the **QueryOrder** enumeration to specify whether to sort ascending or descending.</span></span>  <span data-ttu-id="d9ce8-228">If you are filtering using the ***where*** method, the ***where*** method must be invoked before the ***orderBy*** method.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-228">If you are filtering using the ***where*** method, the ***where*** method must be invoked before the ***orderBy*** method.</span></span>

### <a name="selection"></a><span data-ttu-id="d9ce8-229">Select specific columns</span><span class="sxs-lookup"><span data-stu-id="d9ce8-229">Select specific columns</span></span>

<span data-ttu-id="d9ce8-230">The following code illustrates how to return all items from a table of **ToDoItems**, but only displays the **complete** and **text** fields.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-230">The following code illustrates how to return all items from a table of **ToDoItems**, but only displays the **complete** and **text** fields.</span></span> <span data-ttu-id="d9ce8-231">**mToDoTable** is the reference to the backend table that we created previously.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-231">**mToDoTable** is the reference to the backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="d9ce8-232">The parameters to the select function are the string names of the table's columns that you want to return.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-232">The parameters to the select function are the string names of the table's columns that you want to return.</span></span>  <span data-ttu-id="d9ce8-233">The **select** method needs to follow methods like **where** and **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-233">The **select** method needs to follow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="d9ce8-234">It can be followed by paging methods like **skip** and **top**.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <a name="paging"></a><span data-ttu-id="d9ce8-235">Return data in pages</span><span class="sxs-lookup"><span data-stu-id="d9ce8-235">Return data in pages</span></span>

<span data-ttu-id="d9ce8-236">Data is **ALWAYS** returned in pages.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="d9ce8-237">The maximum number of records returned is set by the server.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-237">The maximum number of records returned is set by the server.</span></span>  <span data-ttu-id="d9ce8-238">If the client requests more records, then the server returns the maximum number of records.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-238">If the client requests more records, then the server returns the maximum number of records.</span></span>  <span data-ttu-id="d9ce8-239">By default, the maximum page size on the server is 50 records.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-239">By default, the maximum page size on the server is 50 records.</span></span>

<span data-ttu-id="d9ce8-240">The first example shows how to select the top five items from a table.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-240">The first example shows how to select the top five items from a table.</span></span> <span data-ttu-id="d9ce8-241">The query returns the items from a table of **ToDoItems**.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-241">The query returns the items from a table of **ToDoItems**.</span></span> <span data-ttu-id="d9ce8-242">**mToDoTable** is the reference to the backend table that you created previously:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-242">**mToDoTable** is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="d9ce8-243">Here's a query that skips the first five items, and then returns the next five:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-243">Here's a query that skips the first five items, and then returns the next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="d9ce8-244">If you wish to get all records in a table, implement code to iterate over all pages:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-244">If you wish to get all records in a table, implement code to iterate over all pages:</span></span>

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

<span data-ttu-id="d9ce8-245">A request for all records using this method creates a minimum of two requests to the Mobile Apps backend.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-245">A request for all records using this method creates a minimum of two requests to the Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="d9ce8-246">Choosing the right page size is a balance between memory usage while the request is happening, bandwidth usage and delay in receiving the data completely.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-246">Choosing the right page size is a balance between memory usage while the request is happening, bandwidth usage and delay in receiving the data completely.</span></span>  <span data-ttu-id="d9ce8-247">The default (50 records) is suitable for all devices.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-247">The default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="d9ce8-248">If you exclusively operate on larger memory devices, increase up to 500.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-248">If you exclusively operate on larger memory devices, increase up to 500.</span></span>  <span data-ttu-id="d9ce8-249">We have found that increasing the page size beyond 500 records results in unacceptable delays and large memory issues.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-249">We have found that increasing the page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <a name="chaining"></a><span data-ttu-id="d9ce8-250">How to: Concatenate query methods</span><span class="sxs-lookup"><span data-stu-id="d9ce8-250">How to: Concatenate query methods</span></span>

<span data-ttu-id="d9ce8-251">The methods used in querying backend tables can be concatenated.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-251">The methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="d9ce8-252">Chaining query methods allows you to select specific columns of filtered rows that are sorted and paged.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-252">Chaining query methods allows you to select specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="d9ce8-253">You can create complex logical filters.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-253">You can create complex logical filters.</span></span>  <span data-ttu-id="d9ce8-254">Each query method returns a Query object.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-254">Each query method returns a Query object.</span></span> <span data-ttu-id="d9ce8-255">To end the series of methods and actually run the query, call the **execute** method.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-255">To end the series of methods and actually run the query, call the **execute** method.</span></span> <span data-ttu-id="d9ce8-256">For example:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-256">For example:</span></span>

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

<span data-ttu-id="d9ce8-257">The chained query methods must be ordered as follows:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-257">The chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="d9ce8-258">Filtering (**where**) methods.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="d9ce8-259">Sorting (**orderBy**) methods.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="d9ce8-260">Selection (**select**) methods.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="d9ce8-261">paging (**skip** and **top**) methods.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-261">paging (**skip** and **top**) methods.</span></span>

## <a name="binding"></a><span data-ttu-id="d9ce8-262">Bind data to the user interface</span><span class="sxs-lookup"><span data-stu-id="d9ce8-262">Bind data to the user interface</span></span>

<span data-ttu-id="d9ce8-263">Data binding involves three components:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-263">Data binding involves three components:</span></span>

* <span data-ttu-id="d9ce8-264">The data source</span><span class="sxs-lookup"><span data-stu-id="d9ce8-264">The data source</span></span>
* <span data-ttu-id="d9ce8-265">The screen layout</span><span class="sxs-lookup"><span data-stu-id="d9ce8-265">The screen layout</span></span>
* <span data-ttu-id="d9ce8-266">The adapter that ties the two together.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-266">The adapter that ties the two together.</span></span>

<span data-ttu-id="d9ce8-267">In our sample code, we return the data from the Mobile Apps SQL Azure table **ToDoItem** into an array.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-267">In our sample code, we return the data from the Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="d9ce8-268">This activity is a common pattern for data applications.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="d9ce8-269">Database queries often return a collection of rows that the client gets in a list or array.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-269">Database queries often return a collection of rows that the client gets in a list or array.</span></span> <span data-ttu-id="d9ce8-270">In this sample, the array is the data source.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-270">In this sample, the array is the data source.</span></span>  <span data-ttu-id="d9ce8-271">The code specifies a screen layout that defines the view of the data that appears on the device.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-271">The code specifies a screen layout that defines the view of the data that appears on the device.</span></span>  <span data-ttu-id="d9ce8-272">The two are bound together with an adapter, which in this code is an extension of the **ArrayAdapter&lt;ToDoItem&gt;** class.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-272">The two are bound together with an adapter, which in this code is an extension of the **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <a name="layout"></a><span data-ttu-id="d9ce8-273">Define the Layout</span><span class="sxs-lookup"><span data-stu-id="d9ce8-273">Define the Layout</span></span>

<span data-ttu-id="d9ce8-274">The layout is defined by several snippets of XML code.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-274">The layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="d9ce8-275">Given an existing layout, the following code represents the **ListView** we want to populate with our server data.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-275">Given an existing layout, the following code represents the **ListView** we want to populate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="d9ce8-276">In the preceding code, the *listitem* attribute specifies the id of the layout for an individual row in the list.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-276">In the preceding code, the *listitem* attribute specifies the id of the layout for an individual row in the list.</span></span> <span data-ttu-id="d9ce8-277">This code specifies a check box and its associated text and gets instantiated once for each item in the list.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-277">This code specifies a check box and its associated text and gets instantiated once for each item in the list.</span></span> <span data-ttu-id="d9ce8-278">This layout does not display the **id** field, and a more complex layout would specify additional fields in the display.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-278">This layout does not display the **id** field, and a more complex layout would specify additional fields in the display.</span></span> <span data-ttu-id="d9ce8-279">This code is in the **row_list_to_do.xml** file.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-279">This code is in the **row_list_to_do.xml** file.</span></span>

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <a name="adapter"></a><span data-ttu-id="d9ce8-280">Define the adapter</span><span class="sxs-lookup"><span data-stu-id="d9ce8-280">Define the adapter</span></span>
<span data-ttu-id="d9ce8-281">Since the data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-281">Since the data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="d9ce8-282">This subclass produces a View for every **ToDoItem** using the **row_list_to_do** layout.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-282">This subclass produces a View for every **ToDoItem** using the **row_list_to_do** layout.</span></span>  <span data-ttu-id="d9ce8-283">In our code, we define the following class that is an extension of the **ArrayAdapter&lt;E&gt;** class:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-283">In our code, we define the following class that is an extension of the **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="d9ce8-284">Override the adapters **getView** method.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-284">Override the adapters **getView** method.</span></span> <span data-ttu-id="d9ce8-285">For example:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-285">For example:</span></span>

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

<span data-ttu-id="d9ce8-286">We create an instance of this class in our Activity as follows:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="d9ce8-287">The second parameter to the ToDoItemAdapter constructor is a reference to the layout.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-287">The second parameter to the ToDoItemAdapter constructor is a reference to the layout.</span></span> <span data-ttu-id="d9ce8-288">We can now instantiate the **ListView** and assign the adapter to the **ListView**.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-288">We can now instantiate the **ListView** and assign the adapter to the **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <a name="use-adapter"></a><span data-ttu-id="d9ce8-289">Use the Adapter to Bind to the UI</span><span class="sxs-lookup"><span data-stu-id="d9ce8-289">Use the Adapter to Bind to the UI</span></span>

<span data-ttu-id="d9ce8-290">You are now ready to use data binding.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-290">You are now ready to use data binding.</span></span> <span data-ttu-id="d9ce8-291">The following code shows how to get items in the table and fills the local adapter with the returned items.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-291">The following code shows how to get items in the table and fills the local adapter with the returned items.</span></span>

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

<span data-ttu-id="d9ce8-292">Call the adapter any time you modify the **ToDoItem** table.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-292">Call the adapter any time you modify the **ToDoItem** table.</span></span> <span data-ttu-id="d9ce8-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="d9ce8-294">When you insert an item, call the **add** method on the adapter; when deleting, call the **remove** method.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-294">When you insert an item, call the **add** method on the adapter; when deleting, call the **remove** method.</span></span>

<span data-ttu-id="d9ce8-295">You can find a complete example in the [Android Quickstart Project][21].</span><span class="sxs-lookup"><span data-stu-id="d9ce8-295">You can find a complete example in the [Android Quickstart Project][21].</span></span>

## <a name="inserting"></a><span data-ttu-id="d9ce8-296">Insert data into the backend</span><span class="sxs-lookup"><span data-stu-id="d9ce8-296">Insert data into the backend</span></span>

<span data-ttu-id="d9ce8-297">Instantiate an instance of the *ToDoItem* class and set its properties.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-297">Instantiate an instance of the *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="d9ce8-298">Then use **insert()** to insert an object:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-298">Then use **insert()** to insert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="d9ce8-299">The returned entity matches the data inserted into the backend table, included the ID and any other values (such as the `createdAt`, `updatedAt`, and `version` fields) set on the backend.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-299">The returned entity matches the data inserted into the backend table, included the ID and any other values (such as the `createdAt`, `updatedAt`, and `version` fields) set on the backend.</span></span>

<span data-ttu-id="d9ce8-300">Mobile Apps tables require a primary key column named **id**. This column must be a string.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-300">Mobile Apps tables require a primary key column named **id**. This column must be a string.</span></span> <span data-ttu-id="d9ce8-301">The default value of the ID column is a GUID.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-301">The default value of the ID column is a GUID.</span></span>  <span data-ttu-id="d9ce8-302">You can provide other unique values, such as email addresses or usernames.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-302">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="d9ce8-303">When a string ID value is not provided for an inserted record, the backend generates a new GUID.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-303">When a string ID value is not provided for an inserted record, the backend generates a new GUID.</span></span>

<span data-ttu-id="d9ce8-304">String ID values provide the following advantages:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-304">String ID values provide the following advantages:</span></span>

* <span data-ttu-id="d9ce8-305">IDs can be generated without making a round trip to the database.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-305">IDs can be generated without making a round trip to the database.</span></span>
* <span data-ttu-id="d9ce8-306">Records are easier to merge from different tables or databases.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-306">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="d9ce8-307">ID values integrate better with an application's logic.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-307">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="d9ce8-308">String ID values are **REQUIRED** for offline sync support.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-308">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="d9ce8-309">You cannot change an Id once it is stored in the backend database.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-309">You cannot change an Id once it is stored in the backend database.</span></span>

## <a name="updating"></a><span data-ttu-id="d9ce8-310">Update data in a mobile app</span><span class="sxs-lookup"><span data-stu-id="d9ce8-310">Update data in a mobile app</span></span>

<span data-ttu-id="d9ce8-311">To update data in a table, pass the new object to the **update()** method.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-311">To update data in a table, pass the new object to the **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="d9ce8-312">In this example, *item* is a reference to a row in the *ToDoItem* table, which has had some changes made to it.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-312">In this example, *item* is a reference to a row in the *ToDoItem* table, which has had some changes made to it.</span></span>  <span data-ttu-id="d9ce8-313">The row with the same **id** is updated.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-313">The row with the same **id** is updated.</span></span>

## <a name="deleting"></a><span data-ttu-id="d9ce8-314">Delete data in a mobile app</span><span class="sxs-lookup"><span data-stu-id="d9ce8-314">Delete data in a mobile app</span></span>

<span data-ttu-id="d9ce8-315">The following code shows how to delete data from a table by specifying the data object.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-315">The following code shows how to delete data from a table by specifying the data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="d9ce8-316">You can also delete an item by specifying the **id** field of the row to delete.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-316">You can also delete an item by specifying the **id** field of the row to delete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <a name="lookup"></a><span data-ttu-id="d9ce8-317">Look up a specific item by Id</span><span class="sxs-lookup"><span data-stu-id="d9ce8-317">Look up a specific item by Id</span></span>

<span data-ttu-id="d9ce8-318">Look up an item with a specific **id** field with the **lookUp()** method:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-318">Look up an item with a specific **id** field with the **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <a name="untyped"></a><span data-ttu-id="d9ce8-319">How to: Work with untyped data</span><span class="sxs-lookup"><span data-stu-id="d9ce8-319">How to: Work with untyped data</span></span>

<span data-ttu-id="d9ce8-320">The untyped programming model gives you exact control over JSON serialization.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-320">The untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="d9ce8-321">There are some common scenarios where you may wish to use an untyped programming model.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-321">There are some common scenarios where you may wish to use an untyped programming model.</span></span> <span data-ttu-id="d9ce8-322">For example, if your backend table contains many columns and you only need to reference a subset of the columns.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-322">For example, if your backend table contains many columns and you only need to reference a subset of the columns.</span></span>  <span data-ttu-id="d9ce8-323">The typed model requires you to define all the columns defined in the Mobile Apps backend in your data class.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-323">The typed model requires you to define all the columns defined in the Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="d9ce8-324">Most of the API calls for accessing data are similar to the typed programming calls.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-324">Most of the API calls for accessing data are similar to the typed programming calls.</span></span> <span data-ttu-id="d9ce8-325">The main difference is that in the untyped model you invoke methods on the **MobileServiceJsonTable** object, instead of the **MobileServiceTable** object.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-325">The main difference is that in the untyped model you invoke methods on the **MobileServiceJsonTable** object, instead of the **MobileServiceTable** object.</span></span>

### <a name="json_instance"></a><span data-ttu-id="d9ce8-326">Create an instance of an untyped table</span><span class="sxs-lookup"><span data-stu-id="d9ce8-326">Create an instance of an untyped table</span></span>

<span data-ttu-id="d9ce8-327">Similar to the typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-327">Similar to the typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="d9ce8-328">Obtain the reference by calling the **getTable** method on an instance of the client:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-328">Obtain the reference by calling the **getTable** method on an instance of the client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="d9ce8-329">Once you have created an instance of the **MobileServiceJsonTable**, it has virtually the same API available as with the typed programming model.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-329">Once you have created an instance of the **MobileServiceJsonTable**, it has virtually the same API available as with the typed programming model.</span></span> <span data-ttu-id="d9ce8-330">In some cases, the methods take an untyped parameter instead of a typed parameter.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-330">In some cases, the methods take an untyped parameter instead of a typed parameter.</span></span>

### <a name="json_insert"></a><span data-ttu-id="d9ce8-331">Insert into an untyped table</span><span class="sxs-lookup"><span data-stu-id="d9ce8-331">Insert into an untyped table</span></span>
<span data-ttu-id="d9ce8-332">The following code shows how to do an insert.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-332">The following code shows how to do an insert.</span></span> <span data-ttu-id="d9ce8-333">The first step is to create a [JsonObject][1], which is part of the [gson][3] library.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-333">The first step is to create a [JsonObject][1], which is part of the [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="d9ce8-334">Then, Use **insert()** to insert the untyped object into the table.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-334">Then, Use **insert()** to insert the untyped object into the table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="d9ce8-335">If you need to get the ID of the inserted object, use the **getAsJsonPrimitive()** method.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-335">If you need to get the ID of the inserted object, use the **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <a name="json_delete"></a><span data-ttu-id="d9ce8-336">Delete from an untyped table</span><span class="sxs-lookup"><span data-stu-id="d9ce8-336">Delete from an untyped table</span></span>
<span data-ttu-id="d9ce8-337">The following code shows how to delete an instance, in this case, the same instance of a **JsonObject** that was created in the prior *insert* example.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-337">The following code shows how to delete an instance, in this case, the same instance of a **JsonObject** that was created in the prior *insert* example.</span></span> <span data-ttu-id="d9ce8-338">The code is the same as with the typed case, but the method has a different signature since it references an **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-338">The code is the same as with the typed case, but the method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="d9ce8-339">You can also delete an instance directly by using its ID:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-339">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <a name="json_get"></a><span data-ttu-id="d9ce8-340">Return all rows from an untyped table</span><span class="sxs-lookup"><span data-stu-id="d9ce8-340">Return all rows from an untyped table</span></span>
<span data-ttu-id="d9ce8-341">The following code shows how to retrieve an entire table.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-341">The following code shows how to retrieve an entire table.</span></span> <span data-ttu-id="d9ce8-342">Since you are using a JSON Table, you can selectively retrieve only some of the table's columns.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-342">Since you are using a JSON Table, you can selectively retrieve only some of the table's columns.</span></span>

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

<span data-ttu-id="d9ce8-343">The same set of filtering, filtering and paging methods that are available for the typed model are available for the untyped model.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-343">The same set of filtering, filtering and paging methods that are available for the typed model are available for the untyped model.</span></span>

## <a name="offline-sync"></a><span data-ttu-id="d9ce8-344">Implement Offline Sync</span><span class="sxs-lookup"><span data-stu-id="d9ce8-344">Implement Offline Sync</span></span>

<span data-ttu-id="d9ce8-345">The Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database to store a copy of the server data locally.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-345">The Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database to store a copy of the server data locally.</span></span>  <span data-ttu-id="d9ce8-346">Operations performed on an offline table do not require mobile connectivity to work.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-346">Operations performed on an offline table do not require mobile connectivity to work.</span></span>  <span data-ttu-id="d9ce8-347">Offline sync aids in resilience and performance at the expense of more complex logic for conflict resolution.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-347">Offline sync aids in resilience and performance at the expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="d9ce8-348">The Azure Mobile Apps Client SDK implements the following features:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-348">The Azure Mobile Apps Client SDK implements the following features:</span></span>

* <span data-ttu-id="d9ce8-349">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-349">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="d9ce8-350">Optimistic Concurrency: Operations are assumed to succeed.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-350">Optimistic Concurrency: Operations are assumed to succeed.</span></span>  <span data-ttu-id="d9ce8-351">Conflict Resolution is deferred until updates are performed on the server.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-351">Conflict Resolution is deferred until updates are performed on the server.</span></span>
* <span data-ttu-id="d9ce8-352">Conflict Resolution: The SDK detects when a conflicting change has been made at the server and provides hooks to alert the user.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-352">Conflict Resolution: The SDK detects when a conflicting change has been made at the server and provides hooks to alert the user.</span></span>
* <span data-ttu-id="d9ce8-353">Soft Delete: Deleted records are marked deleted, allowing other devices to update their offline cache.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-353">Soft Delete: Deleted records are marked deleted, allowing other devices to update their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="d9ce8-354">Initialize Offline Sync</span><span class="sxs-lookup"><span data-stu-id="d9ce8-354">Initialize Offline Sync</span></span>

<span data-ttu-id="d9ce8-355">Each offline table must be defined in the offline cache before use.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-355">Each offline table must be defined in the offline cache before use.</span></span>  <span data-ttu-id="d9ce8-356">Normally, table definition is done immediately after the creation of the client:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-356">Normally, table definition is done immediately after the creation of the client:</span></span>

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with the model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define the table in the local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize the local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-to-the-offline-cache-table"></a><span data-ttu-id="d9ce8-357">Obtain a reference to the Offline Cache Table</span><span class="sxs-lookup"><span data-stu-id="d9ce8-357">Obtain a reference to the Offline Cache Table</span></span>

<span data-ttu-id="d9ce8-358">For an online table, you use `.getTable()`.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-358">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="d9ce8-359">For an offline table, use `.getSyncTable()`:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-359">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceSyncTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="d9ce8-360">All the methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-360">All the methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-the-local-offline-cache"></a><span data-ttu-id="d9ce8-361">Synchronize the Local Offline Cache</span><span class="sxs-lookup"><span data-stu-id="d9ce8-361">Synchronize the Local Offline Cache</span></span>

<span data-ttu-id="d9ce8-362">Synchronization is within the control of your app.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-362">Synchronization is within the control of your app.</span></span>  <span data-ttu-id="d9ce8-363">Here is an example synchronization method:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-363">Here is an example synchronization method:</span></span>

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

<span data-ttu-id="d9ce8-364">If a query name is provided to the `.pull(query, queryname)` method, then incremental sync is used to return only records that have been created or changed since the last successfully completed pull.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-364">If a query name is provided to the `.pull(query, queryname)` method, then incremental sync is used to return only records that have been created or changed since the last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="d9ce8-365">Handle Conflicts during Offline Synchronization</span><span class="sxs-lookup"><span data-stu-id="d9ce8-365">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="d9ce8-366">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-366">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="d9ce8-367">The server-issued item is embedded in the exception and can be retrieved by `.getItem()` on the exception.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-367">The server-issued item is embedded in the exception and can be retrieved by `.getItem()` on the exception.</span></span>  <span data-ttu-id="d9ce8-368">Adjust the push by calling the following items on the MobileServiceSyncContext object:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-368">Adjust the push by calling the following items on the MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="d9ce8-369">Once all conflicts are marked as you wish, call `.push()` again to resolve all the conflicts.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-369">Once all conflicts are marked as you wish, call `.push()` again to resolve all the conflicts.</span></span>

## <a name="custom-api"></a><span data-ttu-id="d9ce8-370">Call a custom API</span><span class="sxs-lookup"><span data-stu-id="d9ce8-370">Call a custom API</span></span>

<span data-ttu-id="d9ce8-371">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-371">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="d9ce8-372">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-372">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="d9ce8-373">From an Android client, you call the **invokeApi** method to call the custom API endpoint.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-373">From an Android client, you call the **invokeApi** method to call the custom API endpoint.</span></span> <span data-ttu-id="d9ce8-374">The following example shows how to call an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-374">The following example shows how to call an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

<span data-ttu-id="d9ce8-375">The **invokeApi** method is called on the client, which sends a POST request to the new custom API.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-375">The **invokeApi** method is called on the client, which sends a POST request to the new custom API.</span></span> <span data-ttu-id="d9ce8-376">The result returned by the custom API is displayed in a message dialog, as are any errors.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-376">The result returned by the custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="d9ce8-377">Other versions of **invokeApi** let you optionally send an object in the request body, specify the HTTP method, and send query parameters with the request.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-377">Other versions of **invokeApi** let you optionally send an object in the request body, specify the HTTP method, and send query parameters with the request.</span></span> <span data-ttu-id="d9ce8-378">Untyped versions of **invokeApi** are provided as well.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-378">Untyped versions of **invokeApi** are provided as well.</span></span>

## <a name="authentication"></a><span data-ttu-id="d9ce8-379">Add authentication to your app</span><span class="sxs-lookup"><span data-stu-id="d9ce8-379">Add authentication to your app</span></span>

<span data-ttu-id="d9ce8-380">Tutorials already describe in detail how to add these features.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-380">Tutorials already describe in detail how to add these features.</span></span>

<span data-ttu-id="d9ce8-381">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-381">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="d9ce8-382">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-382">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="d9ce8-383">You can also use the identity of authenticated users to implement authorization rules in your backend.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-383">You can also use the identity of authenticated users to implement authorization rules in your backend.</span></span>

<span data-ttu-id="d9ce8-384">Two authentication flows are supported: a **server** flow and a **client** flow.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-384">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="d9ce8-385">The server flow provides the simplest authentication experience, as it relies on the identity providers web interface.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-385">The server flow provides the simplest authentication experience, as it relies on the identity providers web interface.</span></span>  <span data-ttu-id="d9ce8-386">No additional SDKs are required to implement server flow authentication.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-386">No additional SDKs are required to implement server flow authentication.</span></span> <span data-ttu-id="d9ce8-387">Server flow authentication does not provide a deep integration into the mobile device and is only recommended for proof of concept scenarios.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-387">Server flow authentication does not provide a deep integration into the mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="d9ce8-388">The client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by the identity provider.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-388">The client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by the identity provider.</span></span>  <span data-ttu-id="d9ce8-389">For example, you can integrate the Facebook SDK into your mobile application.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-389">For example, you can integrate the Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="d9ce8-390">The mobile client swaps into the Facebook app and confirms your sign-on before swapping back to your mobile app.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-390">The mobile client swaps into the Facebook app and confirms your sign-on before swapping back to your mobile app.</span></span>

<span data-ttu-id="d9ce8-391">Four steps are required to enable authentication in your app:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-391">Four steps are required to enable authentication in your app:</span></span>

* <span data-ttu-id="d9ce8-392">Register your app for authentication with an identity provider.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-392">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="d9ce8-393">Configure your App Service backend.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-393">Configure your App Service backend.</span></span>
* <span data-ttu-id="d9ce8-394">Restrict table permissions to authenticated users only on the App Service backend.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-394">Restrict table permissions to authenticated users only on the App Service backend.</span></span>
* <span data-ttu-id="d9ce8-395">Add authentication code to your app.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-395">Add authentication code to your app.</span></span>

<span data-ttu-id="d9ce8-396">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-396">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="d9ce8-397">You can also use the SID of an authenticated user to modify requests.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-397">You can also use the SID of an authenticated user to modify requests.</span></span>  <span data-ttu-id="d9ce8-398">For more information, review [Get started with authentication] and the Server SDK HOWTO documentation.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-398">For more information, review [Get started with authentication] and the Server SDK HOWTO documentation.</span></span>

### <a name="caching"></a><span data-ttu-id="d9ce8-399">Authentication: Server Flow</span><span class="sxs-lookup"><span data-stu-id="d9ce8-399">Authentication: Server Flow</span></span>

<span data-ttu-id="d9ce8-400">The following code starts a server flow login process using the Google provider.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-400">The following code starts a server flow login process using the Google provider.</span></span>  <span data-ttu-id="d9ce8-401">Additional configuration is required because of the security requirements for the Google provider:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-401">Additional configuration is required because of the security requirements for the Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="d9ce8-402">In addition, add the following method to the main Activity class:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-402">In addition, add the following method to the main Activity class:</span></span>

```java
// You can choose any unique number here to differentiate auth providers from each other. Note this is the same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check the request code matches the one we send in the login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check the error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="d9ce8-403">The `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for the `login()` method and within the `onActivityResult()` method.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-403">The `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for the `login()` method and within the `onActivityResult()` method.</span></span>  <span data-ttu-id="d9ce8-404">You can choose any unique number, as long as the same number is used within the `login()` method and the `onActivityResult()` method.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-404">You can choose any unique number, as long as the same number is used within the `login()` method and the `onActivityResult()` method.</span></span>  <span data-ttu-id="d9ce8-405">If you abstract the client code into a service adapter (as shown earlier), you should call the appropriate methods on the service adapter.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-405">If you abstract the client code into a service adapter (as shown earlier), you should call the appropriate methods on the service adapter.</span></span>

<span data-ttu-id="d9ce8-406">You also need to configure the project for customtabs.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-406">You also need to configure the project for customtabs.</span></span>  <span data-ttu-id="d9ce8-407">First specify a redirect-URL.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-407">First specify a redirect-URL.</span></span>  <span data-ttu-id="d9ce8-408">Add the following snippet to `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-408">Add the following snippet to `AndroidManifest.xml`:</span></span>

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

<span data-ttu-id="d9ce8-409">Add the **redirectUriScheme** to the `build.gradle` file for your application:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-409">Add the **redirectUriScheme** to the `build.gradle` file for your application:</span></span>

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

<span data-ttu-id="d9ce8-410">Finally, add `com.android.support:customtabs:23.0.1` to the dependencies list in the `build.gradle` file:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-410">Finally, add `com.android.support:customtabs:23.0.1` to the dependencies list in the `build.gradle` file:</span></span>

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.4.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

<span data-ttu-id="d9ce8-411">Obtain the ID of the logged-in user from a **MobileServiceUser** using the **getUserId** method.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-411">Obtain the ID of the logged-in user from a **MobileServiceUser** using the **getUserId** method.</span></span> <span data-ttu-id="d9ce8-412">For an example of how to use Futures to call the asynchronous login APIs, see [Get started with authentication].</span><span class="sxs-lookup"><span data-stu-id="d9ce8-412">For an example of how to use Futures to call the asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="d9ce8-413">The URL Scheme mentioned is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-413">The URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="d9ce8-414">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-414">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <a name="caching"></a><span data-ttu-id="d9ce8-415">Cache authentication tokens</span><span class="sxs-lookup"><span data-stu-id="d9ce8-415">Cache authentication tokens</span></span>

<span data-ttu-id="d9ce8-416">Caching authentication tokens requires you to store the User ID and authentication token locally on the device.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-416">Caching authentication tokens requires you to store the User ID and authentication token locally on the device.</span></span> <span data-ttu-id="d9ce8-417">The next time the app starts, you check the cache, and if these values are present, you can skip the log in procedure and rehydrate the client with this data.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-417">The next time the app starts, you check the cache, and if these values are present, you can skip the log in procedure and rehydrate the client with this data.</span></span> <span data-ttu-id="d9ce8-418">However this data is sensitive, and it should be stored encrypted for safety in case the phone gets stolen.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-418">However this data is sensitive, and it should be stored encrypted for safety in case the phone gets stolen.</span></span>  <span data-ttu-id="d9ce8-419">You can see a complete example of how to cache authentication tokens in [Cache authentication tokens section][7].</span><span class="sxs-lookup"><span data-stu-id="d9ce8-419">You can see a complete example of how to cache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="d9ce8-420">When you try to use an expired token, you receive a *401 unauthorized* response.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-420">When you try to use an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="d9ce8-421">You can handle authentication errors using filters.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-421">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="d9ce8-422">Filters intercept requests to the App Service backend.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-422">Filters intercept requests to the App Service backend.</span></span> <span data-ttu-id="d9ce8-423">The filter code tests the response for a 401, triggers the sign-in process, and then resumes the request that generated the 401.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-423">The filter code tests the response for a 401, triggers the sign-in process, and then resumes the request that generated the 401.</span></span>

### <a name="refresh"></a><span data-ttu-id="d9ce8-424">Use Refresh Tokens</span><span class="sxs-lookup"><span data-stu-id="d9ce8-424">Use Refresh Tokens</span></span>

<span data-ttu-id="d9ce8-425">The token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-425">The token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="d9ce8-426">After this period, you must reauthenticate the user.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-426">After this period, you must reauthenticate the user.</span></span>  <span data-ttu-id="d9ce8-427">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using the same token.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-427">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using the same token.</span></span>  <span data-ttu-id="d9ce8-428">Another Azure App Service token is generated with a new lifetime.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-428">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="d9ce8-429">You can also register the provider to use Refresh Tokens.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-429">You can also register the provider to use Refresh Tokens.</span></span>  <span data-ttu-id="d9ce8-430">A Refresh Token is not always available.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-430">A Refresh Token is not always available.</span></span>  <span data-ttu-id="d9ce8-431">Additional configuration is required:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-431">Additional configuration is required:</span></span>

* <span data-ttu-id="d9ce8-432">For **Azure Active Directory**, configure a client secret for the Azure Active Directory App.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-432">For **Azure Active Directory**, configure a client secret for the Azure Active Directory App.</span></span>  <span data-ttu-id="d9ce8-433">Specify the client secret in the Azure App Service when configuring Azure Active Directory Authentication.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-433">Specify the client secret in the Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="d9ce8-434">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-434">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="d9ce8-435">For **Google**, pass the `access_type=offline` as a parameter:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-435">For **Google**, pass the `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="d9ce8-436">For **Microsoft Account**, select the `wl.offline_access` scope.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-436">For **Microsoft Account**, select the `wl.offline_access` scope.</span></span>

<span data-ttu-id="d9ce8-437">To refresh a token, call `.refreshUser()`:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-437">To refresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="d9ce8-438">As a best practice, create a filter that detects a 401 response from the server and tries to refresh the user token.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-438">As a best practice, create a filter that detects a 401 response from the server and tries to refresh the user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="d9ce8-439">Log in with Client-flow Authentication</span><span class="sxs-lookup"><span data-stu-id="d9ce8-439">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="d9ce8-440">The general process for logging in with client-flow authentication is as follows:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-440">The general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="d9ce8-441">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-441">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="d9ce8-442">Integrate the authentication provider SDK for authentication to produce an access token.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-442">Integrate the authentication provider SDK for authentication to produce an access token.</span></span>
* <span data-ttu-id="d9ce8-443">Call the `.login()` method as follows:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-443">Call the `.login()` method as follows:</span></span>

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

<span data-ttu-id="d9ce8-444">Replace the `onSuccess()` method with whatever code you wish to use on a successful login.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-444">Replace the `onSuccess()` method with whatever code you wish to use on a successful login.</span></span>  <span data-ttu-id="d9ce8-445">The `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-445">The `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="d9ce8-446">If you have implemented custom authentication, then you can also use the custom authentication provider tag.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-446">If you have implemented custom authentication, then you can also use the custom authentication provider tag.</span></span>

### <a name="adal"></a><span data-ttu-id="d9ce8-447">Authenticate users with the Active Directory Authentication Library (ADAL)</span><span class="sxs-lookup"><span data-stu-id="d9ce8-447">Authenticate users with the Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="d9ce8-448">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-448">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="d9ce8-449">Using a client flow login is often preferable to using the `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-449">Using a client flow login is often preferable to using the `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="d9ce8-450">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][22] tutorial.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-450">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="d9ce8-451">Make sure to complete the optional step of registering a native client application.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-451">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="d9ce8-452">Install ADAL by modifying your build.gradle file to include the following definitions:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-452">Install ADAL by modifying your build.gradle file to include the following definitions:</span></span>

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. <span data-ttu-id="d9ce8-453">Add the following code to your application, making the following replacements:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-453">Add the following code to your application, making the following replacements:</span></span>

* <span data-ttu-id="d9ce8-454">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-454">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="d9ce8-455">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-455">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="d9ce8-456">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-456">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="d9ce8-457">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-457">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
* <span data-ttu-id="d9ce8-458">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-458">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
* <span data-ttu-id="d9ce8-459">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-459">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="d9ce8-460">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-460">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <a name="filters"></a><span data-ttu-id="d9ce8-461">Adjust the Client-Server Communication</span><span class="sxs-lookup"><span data-stu-id="d9ce8-461">Adjust the Client-Server Communication</span></span>

<span data-ttu-id="d9ce8-462">The Client connection is normally a basic HTTP connection using the underlying HTTP library supplied with the Android SDK.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-462">The Client connection is normally a basic HTTP connection using the underlying HTTP library supplied with the Android SDK.</span></span>  <span data-ttu-id="d9ce8-463">There are several reasons why you would want to change that:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-463">There are several reasons why you would want to change that:</span></span>

* <span data-ttu-id="d9ce8-464">You wish to use an alternate HTTP library to adjust timeouts.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-464">You wish to use an alternate HTTP library to adjust timeouts.</span></span>
* <span data-ttu-id="d9ce8-465">You wish to provide a progress bar.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-465">You wish to provide a progress bar.</span></span>
* <span data-ttu-id="d9ce8-466">You wish to add a custom header to support API management functionality.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-466">You wish to add a custom header to support API management functionality.</span></span>
* <span data-ttu-id="d9ce8-467">You wish to intercept a failed response so that you can implement reauthentication.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-467">You wish to intercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="d9ce8-468">You wish to log backend requests to an analytics service.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-468">You wish to log backend requests to an analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="d9ce8-469">Using an alternate HTTP Library</span><span class="sxs-lookup"><span data-stu-id="d9ce8-469">Using an alternate HTTP Library</span></span>

<span data-ttu-id="d9ce8-470">Call the `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-470">Call the `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="d9ce8-471">For example, to set the connection timeout to 60 seconds (instead of the default 10 seconds):</span><span class="sxs-lookup"><span data-stu-id="d9ce8-471">For example, to set the connection timeout to 60 seconds (instead of the default 10 seconds):</span></span>

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a><span data-ttu-id="d9ce8-472">Implement a Progress Filter</span><span class="sxs-lookup"><span data-stu-id="d9ce8-472">Implement a Progress Filter</span></span>

<span data-ttu-id="d9ce8-473">You can implement an intercept of every request by implementing a `ServiceFilter`.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-473">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="d9ce8-474">For example, the following updates a pre-created progress bar:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-474">For example, the following updates a pre-created progress bar:</span></span>

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

<span data-ttu-id="d9ce8-475">You can attach this filter to the client as follows:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-475">You can attach this filter to the client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="d9ce8-476">Customize Request Headers</span><span class="sxs-lookup"><span data-stu-id="d9ce8-476">Customize Request Headers</span></span>

<span data-ttu-id="d9ce8-477">Use the following `ServiceFilter` and attach the filter in the same way as the `ProgressFilter`:</span><span class="sxs-lookup"><span data-stu-id="d9ce8-477">Use the following `ServiceFilter` and attach the filter in the same way as the `ProgressFilter`:</span></span>

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <a name="conversions"></a><span data-ttu-id="d9ce8-478">Configure Automatic Serialization</span><span class="sxs-lookup"><span data-stu-id="d9ce8-478">Configure Automatic Serialization</span></span>

<span data-ttu-id="d9ce8-479">You can specify a conversion strategy that applies to every column by using the [gson][3] API.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-479">You can specify a conversion strategy that applies to every column by using the [gson][3] API.</span></span> <span data-ttu-id="d9ce8-480">The Android client library uses [gson][3] behind the scenes to serialize Java objects to JSON data before the data is sent to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-480">The Android client library uses [gson][3] behind the scenes to serialize Java objects to JSON data before the data is sent to Azure App Service.</span></span>  <span data-ttu-id="d9ce8-481">The following code uses the **setFieldNamingStrategy()** method to set the strategy.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-481">The following code uses the **setFieldNamingStrategy()** method to set the strategy.</span></span> <span data-ttu-id="d9ce8-482">This example will delete the initial character (an "m"), and then lower-case the next character, for every field name.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-482">This example will delete the initial character (an "m"), and then lower-case the next character, for every field name.</span></span> <span data-ttu-id="d9ce8-483">For example, it would turn "mId" into "id."</span><span class="sxs-lookup"><span data-stu-id="d9ce8-483">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="d9ce8-484">Implement a conversion strategy to reduce the need for `SerializedName()` annotations on most fields.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-484">Implement a conversion strategy to reduce the need for `SerializedName()` annotations on most fields.</span></span>

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

<span data-ttu-id="d9ce8-485">This code must be executed before creating a mobile client reference using the **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="d9ce8-485">This code must be executed before creating a mobile client reference using the **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[Get started with authentication]: app-service-mobile-android-get-started-users.md
[1]: https://static.javadoc.io/com.google.code.gson/gson/2.8.5/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: https://www.javadoc.io/doc/com.google.code.gson/gson/2.8.5
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: ../app-service/app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
