---
title: How to use the Android Mobile Apps Client Library
description: How to use Android client SDK for Azure Mobile Apps.
services: app-service\mobile
documentationcenter: android
author: ysxu
manager: adrianha
editor: ''
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: 277df83870c9cbfcb2407999ca9bc6a799284abe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660767"
---
# <a name="how-to-use-the-android-client-library-for-mobile-apps"></a><span data-ttu-id="3c586-103">How to use the Android client library for Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="3c586-103">How to use the Android client library for Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="3c586-104">This guide shows you how to use the Android client SDK for Mobile Apps to implement common scenarios, such as:</span><span class="sxs-lookup"><span data-stu-id="3c586-104">This guide shows you how to use the Android client SDK for Mobile Apps to implement common scenarios, such as:</span></span>

* <span data-ttu-id="3c586-105">Querying for data (inserting, updating, and deleting).</span><span class="sxs-lookup"><span data-stu-id="3c586-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="3c586-106">Authentication.</span><span class="sxs-lookup"><span data-stu-id="3c586-106">Authentication.</span></span>
* <span data-ttu-id="3c586-107">Handling errors.</span><span class="sxs-lookup"><span data-stu-id="3c586-107">Handling errors.</span></span>
* <span data-ttu-id="3c586-108">Customizing the client.</span><span class="sxs-lookup"><span data-stu-id="3c586-108">Customizing the client.</span></span>

<span data-ttu-id="3c586-109">It also does a deep-dive into common client code used in most mobile apps.</span><span class="sxs-lookup"><span data-stu-id="3c586-109">It also does a deep-dive into common client code used in most mobile apps.</span></span>

<span data-ttu-id="3c586-110">This guide focuses on the client-side Android SDK.</span><span class="sxs-lookup"><span data-stu-id="3c586-110">This guide focuses on the client-side Android SDK.</span></span>  <span data-ttu-id="3c586-111">To learn more about the server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How to use the Node.js backend SDK][11].</span><span class="sxs-lookup"><span data-stu-id="3c586-111">To learn more about the server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How to use the Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="3c586-112">Reference Documentation</span><span class="sxs-lookup"><span data-stu-id="3c586-112">Reference Documentation</span></span>
<span data-ttu-id="3c586-113">You can find the [Javadocs API reference][12] for the Android client library on GitHub.</span><span class="sxs-lookup"><span data-stu-id="3c586-113">You can find the [Javadocs API reference][12] for the Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="3c586-114">Supported Platforms</span><span class="sxs-lookup"><span data-stu-id="3c586-114">Supported Platforms</span></span>
<span data-ttu-id="3c586-115">The Azure Mobile Apps Android SDK supports API levels 19 through 24 (KitKat through Nougat).</span><span class="sxs-lookup"><span data-stu-id="3c586-115">The Azure Mobile Apps Android SDK supports API levels 19 through 24 (KitKat through Nougat).</span></span>  

<span data-ttu-id="3c586-116">The "server-flow" authentication uses a WebView for the presented UI.</span><span class="sxs-lookup"><span data-stu-id="3c586-116">The "server-flow" authentication uses a WebView for the presented UI.</span></span> <span data-ttu-id="3c586-117">If the device is not able to present a WebView UI, then other methods of authentication are needed that is outside the scope of the product.</span><span class="sxs-lookup"><span data-stu-id="3c586-117">If the device is not able to present a WebView UI, then other methods of authentication are needed that is outside the scope of the product.</span></span>  <span data-ttu-id="3c586-118">This SDK is not suitable for Watch-type or similarly restricted devices.</span><span class="sxs-lookup"><span data-stu-id="3c586-118">This SDK is not suitable for Watch-type or similarly restricted devices.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="3c586-119">Setup and Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3c586-119">Setup and Prerequisites</span></span>
<span data-ttu-id="3c586-120">Complete the [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="3c586-120">Complete the [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="3c586-121">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span><span class="sxs-lookup"><span data-stu-id="3c586-121">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="3c586-122">The Quickstart also helps you configure your account and create your first Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="3c586-122">The Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="3c586-123">If you decide not to complete the Quickstart tutorial, complete the following tasks:</span><span class="sxs-lookup"><span data-stu-id="3c586-123">If you decide not to complete the Quickstart tutorial, complete the following tasks:</span></span>

* <span data-ttu-id="3c586-124">[create a Mobile App backend][13] to use with your Android app.</span><span class="sxs-lookup"><span data-stu-id="3c586-124">[create a Mobile App backend][13] to use with your Android app.</span></span>
* <span data-ttu-id="3c586-125">In Android Studio, [update the Gradle build files](#gradle-build).</span><span class="sxs-lookup"><span data-stu-id="3c586-125">In Android Studio, [update the Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="3c586-126">[Enable internet permission](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="3c586-126">[Enable internet permission](#enable-internet).</span></span>

### <a name="gradle-build"></a><span data-ttu-id="3c586-127">Update the Gradle build file</span><span class="sxs-lookup"><span data-stu-id="3c586-127">Update the Gradle build file</span></span>
<span data-ttu-id="3c586-128">Change both **build.gradle** files:</span><span class="sxs-lookup"><span data-stu-id="3c586-128">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="3c586-129">Add this code to the *Project* level **build.gradle** file inside the *buildscript* tag:</span><span class="sxs-lookup"><span data-stu-id="3c586-129">Add this code to the *Project* level **build.gradle** file inside the *buildscript* tag:</span></span>

        buildscript {
            repositories {
                jcenter()
            }
        }
2. <span data-ttu-id="3c586-130">Add this code to the *Module app* level **build.gradle** file inside the *dependencies* tag:</span><span class="sxs-lookup"><span data-stu-id="3c586-130">Add this code to the *Module app* level **build.gradle** file inside the *dependencies* tag:</span></span>

        compile 'com.microsoft.azure:azure-mobile-android:3.1.0'

    <span data-ttu-id="3c586-131">Currently the latest version is 3.1.0.</span><span class="sxs-lookup"><span data-stu-id="3c586-131">Currently the latest version is 3.1.0.</span></span> <span data-ttu-id="3c586-132">The supported versions are listed [here][14].</span><span class="sxs-lookup"><span data-stu-id="3c586-132">The supported versions are listed [here][14].</span></span>

### <a name="enable-internet"></a><span data-ttu-id="3c586-133">Enable internet permission</span><span class="sxs-lookup"><span data-stu-id="3c586-133">Enable internet permission</span></span>
<span data-ttu-id="3c586-134">To access Azure, your app must have the INTERNET permission enabled.</span><span class="sxs-lookup"><span data-stu-id="3c586-134">To access Azure, your app must have the INTERNET permission enabled.</span></span> <span data-ttu-id="3c586-135">If it's not already enabled, add the following line of code to your **AndroidManifest.xml** file:</span><span class="sxs-lookup"><span data-stu-id="3c586-135">If it's not already enabled, add the following line of code to your **AndroidManifest.xml** file:</span></span>

    <uses-permission android:name="android.permission.INTERNET" />

## <a name="the-basics-deep-dive"></a><span data-ttu-id="3c586-136">The basics deep dive</span><span class="sxs-lookup"><span data-stu-id="3c586-136">The basics deep dive</span></span>
<span data-ttu-id="3c586-137">This section discusses some of the code in the Quickstart app that pertains to using Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="3c586-137">This section discusses some of the code in the Quickstart app that pertains to using Azure Mobile Apps.</span></span>  

### <a name="data-object"></a><span data-ttu-id="3c586-138">Define client data classes</span><span class="sxs-lookup"><span data-stu-id="3c586-138">Define client data classes</span></span>
<span data-ttu-id="3c586-139">To access data from SQL Azure tables, define client data classes that correspond to the tables in the Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="3c586-139">To access data from SQL Azure tables, define client data classes that correspond to the tables in the Mobile App backend.</span></span> <span data-ttu-id="3c586-140">Examples in this topic assume a table named **ToDoItem**, which has the following columns:</span><span class="sxs-lookup"><span data-stu-id="3c586-140">Examples in this topic assume a table named **ToDoItem**, which has the following columns:</span></span>

* <span data-ttu-id="3c586-141">id</span><span class="sxs-lookup"><span data-stu-id="3c586-141">id</span></span>
* <span data-ttu-id="3c586-142">text</span><span class="sxs-lookup"><span data-stu-id="3c586-142">text</span></span>
* <span data-ttu-id="3c586-143">complete</span><span class="sxs-lookup"><span data-stu-id="3c586-143">complete</span></span>

<span data-ttu-id="3c586-144">The corresponding typed client-side object:</span><span class="sxs-lookup"><span data-stu-id="3c586-144">The corresponding typed client-side object:</span></span>

    public class ToDoItem {
        private String id;
        private String text;
        private Boolean complete;
    }

<span data-ttu-id="3c586-145">The code resides in a file called **ToDoItem.java**.</span><span class="sxs-lookup"><span data-stu-id="3c586-145">The code resides in a file called **ToDoItem.java**.</span></span>

<span data-ttu-id="3c586-146">If your SQL Azure table contains more columns, you would add the corresponding fields to this class.</span><span class="sxs-lookup"><span data-stu-id="3c586-146">If your SQL Azure table contains more columns, you would add the corresponding fields to this class.</span></span>  <span data-ttu-id="3c586-147">For example, if the DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span><span class="sxs-lookup"><span data-stu-id="3c586-147">For example, if the DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

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

<span data-ttu-id="3c586-148">To learn how to create additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span><span class="sxs-lookup"><span data-stu-id="3c586-148">To learn how to create additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span> <span data-ttu-id="3c586-149">For a Node.js backend, you can also use the **Easy tables** setting in the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="3c586-149">For a Node.js backend, you can also use the **Easy tables** setting in the [Azure portal].</span></span>

### <a name="create-client"></a><span data-ttu-id="3c586-150">How to: Create the client context</span><span class="sxs-lookup"><span data-stu-id="3c586-150">How to: Create the client context</span></span>
<span data-ttu-id="3c586-151">This code creates the **MobileServiceClient** object that is used to access your Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="3c586-151">This code creates the **MobileServiceClient** object that is used to access your Mobile App backend.</span></span> <span data-ttu-id="3c586-152">The code goes in the `onCreate` method of the **Activity** class specified in *AndroidManifest.xml* as a **MAIN** action and **LAUNCHER** category.</span><span class="sxs-lookup"><span data-stu-id="3c586-152">The code goes in the `onCreate` method of the **Activity** class specified in *AndroidManifest.xml* as a **MAIN** action and **LAUNCHER** category.</span></span> <span data-ttu-id="3c586-153">In the Quickstart code, it goes in the **ToDoActivity.java** file.</span><span class="sxs-lookup"><span data-stu-id="3c586-153">In the Quickstart code, it goes in the **ToDoActivity.java** file.</span></span>

        MobileServiceClient mClient = new MobileServiceClient(
            "MobileAppUrl", // Replace with the Site URL
            this)

<span data-ttu-id="3c586-154">In this code, replace `MobileAppUrl` with the URL of your Mobile App backend, which can be found in the [Azure portal] in the blade for your Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="3c586-154">In this code, replace `MobileAppUrl` with the URL of your Mobile App backend, which can be found in the [Azure portal] in the blade for your Mobile App backend.</span></span> <span data-ttu-id="3c586-155">For this line of code to compile, you also need to add the following **import** statement:</span><span class="sxs-lookup"><span data-stu-id="3c586-155">For this line of code to compile, you also need to add the following **import** statement:</span></span>

    import com.microsoft.windowsazure.mobileservices.*;

### <a name="instantiating"></a><span data-ttu-id="3c586-156">How to: Create a table reference</span><span class="sxs-lookup"><span data-stu-id="3c586-156">How to: Create a table reference</span></span>
<span data-ttu-id="3c586-157">The easiest way to query or modify data in the backend is by using the *typed programming model*, since Java is a strongly typed language.</span><span class="sxs-lookup"><span data-stu-id="3c586-157">The easiest way to query or modify data in the backend is by using the *typed programming model*, since Java is a strongly typed language.</span></span> <span data-ttu-id="3c586-158">This model provides seamless JSON serialization and deserialization using the [gson][3] library when sending data between client objects and tables in the backend Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="3c586-158">This model provides seamless JSON serialization and deserialization using the [gson][3] library when sending data between client objects and tables in the backend Azure SQL.</span></span>

<span data-ttu-id="3c586-159">To access a table, first create a [MobileServiceTable][8] object by calling the **getTable** method on the [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="3c586-159">To access a table, first create a [MobileServiceTable][8] object by calling the **getTable** method on the [MobileServiceClient][9].</span></span>  <span data-ttu-id="3c586-160">This method has two overloads:</span><span class="sxs-lookup"><span data-stu-id="3c586-160">This method has two overloads:</span></span>

    public class MobileServiceClient {
        public <E> MobileServiceTable<E> getTable(Class<E> clazz);
        public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
    }

<span data-ttu-id="3c586-161">In the following code, **mClient** is a reference to your MobileServiceClient object.</span><span class="sxs-lookup"><span data-stu-id="3c586-161">In the following code, **mClient** is a reference to your MobileServiceClient object.</span></span>  <span data-ttu-id="3c586-162">The first overload is used where the class name and the table name are the same, and is the one used in the Quickstart:</span><span class="sxs-lookup"><span data-stu-id="3c586-162">The first overload is used where the class name and the table name are the same, and is the one used in the Quickstart:</span></span>

    MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);

<span data-ttu-id="3c586-163">The second overload is used when the table name is different from the class name: the first parameter is the table name.</span><span class="sxs-lookup"><span data-stu-id="3c586-163">The second overload is used when the table name is different from the class name: the first parameter is the table name.</span></span>

    MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);

### <a name="binding"></a><span data-ttu-id="3c586-164">How to: Bind data to the user interface</span><span class="sxs-lookup"><span data-stu-id="3c586-164">How to: Bind data to the user interface</span></span>
<span data-ttu-id="3c586-165">Data binding involves three components:</span><span class="sxs-lookup"><span data-stu-id="3c586-165">Data binding involves three components:</span></span>

* <span data-ttu-id="3c586-166">The data source</span><span class="sxs-lookup"><span data-stu-id="3c586-166">The data source</span></span>
* <span data-ttu-id="3c586-167">The screen layout</span><span class="sxs-lookup"><span data-stu-id="3c586-167">The screen layout</span></span>
* <span data-ttu-id="3c586-168">The adapter that ties the two together.</span><span class="sxs-lookup"><span data-stu-id="3c586-168">The adapter that ties the two together.</span></span>

<span data-ttu-id="3c586-169">In our sample code, we return the data from the Mobile Apps SQL Azure table **ToDoItem** into an array.</span><span class="sxs-lookup"><span data-stu-id="3c586-169">In our sample code, we return the data from the Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="3c586-170">This activity is a common pattern for data applications.</span><span class="sxs-lookup"><span data-stu-id="3c586-170">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="3c586-171">Database queries often return a collection of rows that the client gets in a list or array.</span><span class="sxs-lookup"><span data-stu-id="3c586-171">Database queries often return a collection of rows that the client gets in a list or array.</span></span> <span data-ttu-id="3c586-172">In this sample, the array is the data source.</span><span class="sxs-lookup"><span data-stu-id="3c586-172">In this sample, the array is the data source.</span></span>

<span data-ttu-id="3c586-173">The code specifies a screen layout that defines the view of the data that appears on the device.</span><span class="sxs-lookup"><span data-stu-id="3c586-173">The code specifies a screen layout that defines the view of the data that appears on the device.</span></span>  <span data-ttu-id="3c586-174">The two are bound together with an adapter, which in this code is an extension of the **ArrayAdapter&lt;ToDoItem&gt;** class.</span><span class="sxs-lookup"><span data-stu-id="3c586-174">The two are bound together with an adapter, which in this code is an extension of the **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <a name="layout"></a><span data-ttu-id="3c586-175">How to: Define the Layout</span><span class="sxs-lookup"><span data-stu-id="3c586-175">How to: Define the Layout</span></span>
<span data-ttu-id="3c586-176">The layout is defined by several snippets of XML code.</span><span class="sxs-lookup"><span data-stu-id="3c586-176">The layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="3c586-177">Given an existing layout, the following code represents the **ListView** we want to populate with our server data.</span><span class="sxs-lookup"><span data-stu-id="3c586-177">Given an existing layout, the following code represents the **ListView** we want to populate with our server data.</span></span>

    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>

<span data-ttu-id="3c586-178">In the preceding code, the *listitem* attribute specifies the id of the layout for an individual row in the list.</span><span class="sxs-lookup"><span data-stu-id="3c586-178">In the preceding code, the *listitem* attribute specifies the id of the layout for an individual row in the list.</span></span> <span data-ttu-id="3c586-179">This code specifies a check box and its associated text and gets instantiated once for each item in the list.</span><span class="sxs-lookup"><span data-stu-id="3c586-179">This code specifies a check box and its associated text and gets instantiated once for each item in the list.</span></span> <span data-ttu-id="3c586-180">This layout does not display the **id** field, and a more complex layout would specify additional fields in the display.</span><span class="sxs-lookup"><span data-stu-id="3c586-180">This layout does not display the **id** field, and a more complex layout would specify additional fields in the display.</span></span> <span data-ttu-id="3c586-181">This code is in the **row_list_to_do.xml** file.</span><span class="sxs-lookup"><span data-stu-id="3c586-181">This code is in the **row_list_to_do.xml** file.</span></span>

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


#### <a name="adapter"></a><span data-ttu-id="3c586-182">How to: Define the adapter</span><span class="sxs-lookup"><span data-stu-id="3c586-182">How to: Define the adapter</span></span>
<span data-ttu-id="3c586-183">Since the data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span><span class="sxs-lookup"><span data-stu-id="3c586-183">Since the data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="3c586-184">This subclass produces a View for every **ToDoItem** using the **row_list_to_do** layout.</span><span class="sxs-lookup"><span data-stu-id="3c586-184">This subclass produces a View for every **ToDoItem** using the **row_list_to_do** layout.</span></span>

<span data-ttu-id="3c586-185">In our code we define the following class that is an extension of the **ArrayAdapter&lt;E&gt;** class:</span><span class="sxs-lookup"><span data-stu-id="3c586-185">In our code we define the following class that is an extension of the **ArrayAdapter&lt;E&gt;** class:</span></span>

    public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {

<span data-ttu-id="3c586-186">Override the adapters **getView** method.</span><span class="sxs-lookup"><span data-stu-id="3c586-186">Override the adapters **getView** method.</span></span> <span data-ttu-id="3c586-187">For example:</span><span class="sxs-lookup"><span data-stu-id="3c586-187">For example:</span></span>

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

<span data-ttu-id="3c586-188">We create an instance of this class in our Activity as follows:</span><span class="sxs-lookup"><span data-stu-id="3c586-188">We create an instance of this class in our Activity as follows:</span></span>

    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);

<span data-ttu-id="3c586-189">The second parameter to the ToDoItemAdapter constructor is a reference to the layout.</span><span class="sxs-lookup"><span data-stu-id="3c586-189">The second parameter to the ToDoItemAdapter constructor is a reference to the layout.</span></span> <span data-ttu-id="3c586-190">We can now instantiate the **ListView** and assign the adapter to the **ListView**.</span><span class="sxs-lookup"><span data-stu-id="3c586-190">We can now instantiate the **ListView** and assign the adapter to the **ListView**.</span></span>

    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);

### <a name="api"></a><span data-ttu-id="3c586-191">The API structure</span><span class="sxs-lookup"><span data-stu-id="3c586-191">The API structure</span></span>
<span data-ttu-id="3c586-192">Mobile Apps table operations and custom API calls are asynchronous.</span><span class="sxs-lookup"><span data-stu-id="3c586-192">Mobile Apps table operations and custom API calls are asynchronous.</span></span> <span data-ttu-id="3c586-193">Use the [Future] and [AsyncTask] objects for the asynchronous methods involving queries, inserts, updates, and deletes.</span><span class="sxs-lookup"><span data-stu-id="3c586-193">Use the [Future] and [AsyncTask] objects for the asynchronous methods involving queries, inserts, updates, and deletes.</span></span> <span data-ttu-id="3c586-194">Using futures makes it easier to perform multiple operations on a background thread without having to deal with multiple nested callbacks.</span><span class="sxs-lookup"><span data-stu-id="3c586-194">Using futures makes it easier to perform multiple operations on a background thread without having to deal with multiple nested callbacks.</span></span>

<span data-ttu-id="3c586-195">Review the **ToDoActivity.java** file in the Android quickstart project from the [Azure portal] for an example.</span><span class="sxs-lookup"><span data-stu-id="3c586-195">Review the **ToDoActivity.java** file in the Android quickstart project from the [Azure portal] for an example.</span></span>

#### <a name="use-adapter"></a><span data-ttu-id="3c586-196">How to: Use the adapter</span><span class="sxs-lookup"><span data-stu-id="3c586-196">How to: Use the adapter</span></span>
<span data-ttu-id="3c586-197">You are now ready to use data binding.</span><span class="sxs-lookup"><span data-stu-id="3c586-197">You are now ready to use data binding.</span></span> <span data-ttu-id="3c586-198">The following code shows how to get items in the table and fills the local adapter with the returned items.</span><span class="sxs-lookup"><span data-stu-id="3c586-198">The following code shows how to get items in the table and fills the local adapter with the returned items.</span></span>

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

<span data-ttu-id="3c586-199">Call the adapter any time you modify the **ToDoItem** table.</span><span class="sxs-lookup"><span data-stu-id="3c586-199">Call the adapter any time you modify the **ToDoItem** table.</span></span> <span data-ttu-id="3c586-200">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span><span class="sxs-lookup"><span data-stu-id="3c586-200">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="3c586-201">When you insert an item, call the **add** method on the adapter; when deleting, call the **remove** method.</span><span class="sxs-lookup"><span data-stu-id="3c586-201">When you insert an item, call the **add** method on the adapter; when deleting, call the **remove** method.</span></span>

## <a name="querying"></a><span data-ttu-id="3c586-202">How to: Query data from your Mobile App backend</span><span class="sxs-lookup"><span data-stu-id="3c586-202">How to: Query data from your Mobile App backend</span></span>
<span data-ttu-id="3c586-203">This section describes how to issue queries to the Mobile App backend, which includes the following tasks:</span><span class="sxs-lookup"><span data-stu-id="3c586-203">This section describes how to issue queries to the Mobile App backend, which includes the following tasks:</span></span>

* <span data-ttu-id="3c586-204">[Return all Items]</span><span class="sxs-lookup"><span data-stu-id="3c586-204">[Return all Items]</span></span>
* <span data-ttu-id="3c586-205">[Filter returned data]</span><span class="sxs-lookup"><span data-stu-id="3c586-205">[Filter returned data]</span></span>
* <span data-ttu-id="3c586-206">[Sort returned data]</span><span class="sxs-lookup"><span data-stu-id="3c586-206">[Sort returned data]</span></span>
* <span data-ttu-id="3c586-207">[Return data in pages]</span><span class="sxs-lookup"><span data-stu-id="3c586-207">[Return data in pages]</span></span>
* <span data-ttu-id="3c586-208">[Select specific columns]</span><span class="sxs-lookup"><span data-stu-id="3c586-208">[Select specific columns]</span></span>
* [<span data-ttu-id="3c586-209">Concatenate query methods</span><span class="sxs-lookup"><span data-stu-id="3c586-209">Concatenate query methods</span></span>](#chaining)

### <a name="showAll"></a><span data-ttu-id="3c586-210">How to: Return all Items from a Table</span><span class="sxs-lookup"><span data-stu-id="3c586-210">How to: Return all Items from a Table</span></span>
<span data-ttu-id="3c586-211">The following query returns all items in the **ToDoItem** table.</span><span class="sxs-lookup"><span data-stu-id="3c586-211">The following query returns all items in the **ToDoItem** table.</span></span>

    List<ToDoItem> results = mToDoTable.execute().get();

<span data-ttu-id="3c586-212">The *results* variable returns the result set from the query as a list.</span><span class="sxs-lookup"><span data-stu-id="3c586-212">The *results* variable returns the result set from the query as a list.</span></span>

### <a name="filtering"></a><span data-ttu-id="3c586-213">How to: Filter returned data</span><span class="sxs-lookup"><span data-stu-id="3c586-213">How to: Filter returned data</span></span>
<span data-ttu-id="3c586-214">The following query execution returns all items from the **ToDoItem** table where **complete** equals **false**.</span><span class="sxs-lookup"><span data-stu-id="3c586-214">The following query execution returns all items from the **ToDoItem** table where **complete** equals **false**.</span></span>

    List<ToDoItem> result = mToDoTable.where()
                                .field("complete").eq(false)
                                .execute().get();

<span data-ttu-id="3c586-215">**mToDoTable** is the reference to the mobile service table that we created previously.</span><span class="sxs-lookup"><span data-stu-id="3c586-215">**mToDoTable** is the reference to the mobile service table that we created previously.</span></span>

<span data-ttu-id="3c586-216">Define a filter using the **where** method call on the table reference.</span><span class="sxs-lookup"><span data-stu-id="3c586-216">Define a filter using the **where** method call on the table reference.</span></span> <span data-ttu-id="3c586-217">The **where** method is followed by a **field** method followed by a method that specifies the logical predicate.</span><span class="sxs-lookup"><span data-stu-id="3c586-217">The **where** method is followed by a **field** method followed by a method that specifies the logical predicate.</span></span> <span data-ttu-id="3c586-218">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span><span class="sxs-lookup"><span data-stu-id="3c586-218">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="3c586-219">These methods let you compare number and string fields to specific values.</span><span class="sxs-lookup"><span data-stu-id="3c586-219">These methods let you compare number and string fields to specific values.</span></span>

<span data-ttu-id="3c586-220">You can filter on dates.</span><span class="sxs-lookup"><span data-stu-id="3c586-220">You can filter on dates.</span></span> <span data-ttu-id="3c586-221">The following methods let you compare the entire date field or parts of the date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span><span class="sxs-lookup"><span data-stu-id="3c586-221">The following methods let you compare the entire date field or parts of the date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="3c586-222">The following example adds a filter for items whose *due date* equals 2013.</span><span class="sxs-lookup"><span data-stu-id="3c586-222">The following example adds a filter for items whose *due date* equals 2013.</span></span>

    mToDoTable.where().year("due").eq(2013).execute().get();

<span data-ttu-id="3c586-223">The following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span><span class="sxs-lookup"><span data-stu-id="3c586-223">The following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="3c586-224">The following example filters for table rows where the *text* column starts with "PRI0."</span><span class="sxs-lookup"><span data-stu-id="3c586-224">The following example filters for table rows where the *text* column starts with "PRI0."</span></span>

    mToDoTable.where().startsWith("text", "PRI0").execute().get();

<span data-ttu-id="3c586-225">The following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span><span class="sxs-lookup"><span data-stu-id="3c586-225">The following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="3c586-226">The following example filters for table rows where the **duration** is an even number.</span><span class="sxs-lookup"><span data-stu-id="3c586-226">The following example filters for table rows where the **duration** is an even number.</span></span>

    mToDoTable.where().field("duration").mod(2).eq(0).execute().get();

<span data-ttu-id="3c586-227">You can combine predicates with these logical methods: **and**, **or** and **not**.</span><span class="sxs-lookup"><span data-stu-id="3c586-227">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="3c586-228">The following example combines two of the preceding examples.</span><span class="sxs-lookup"><span data-stu-id="3c586-228">The following example combines two of the preceding examples.</span></span>

    mToDoTable.where().year("due").eq(2013).and().startsWith("text", "PRI0")
                .execute().get();

<span data-ttu-id="3c586-229">Group and nest logical operators:</span><span class="sxs-lookup"><span data-stu-id="3c586-229">Group and nest logical operators:</span></span>

    mToDoTable.where()
                .year("due").eq(2013)
                    .and
                (startsWith("text", "PRI0").or().field("duration").gt(10))
                .execute().get();

<span data-ttu-id="3c586-230">For more detailed discussion and examples of filtering, see [Exploring the richness of the Android client query model](http://hashtagfail.com/post/46493261719/mobile-services-android-querying).</span><span class="sxs-lookup"><span data-stu-id="3c586-230">For more detailed discussion and examples of filtering, see [Exploring the richness of the Android client query model](http://hashtagfail.com/post/46493261719/mobile-services-android-querying).</span></span>

### <a name="sorting"></a><span data-ttu-id="3c586-231">How to: Sort returned data</span><span class="sxs-lookup"><span data-stu-id="3c586-231">How to: Sort returned data</span></span>
<span data-ttu-id="3c586-232">The following code returns all items from a table of **ToDoItems** sorted ascending by the *text* field.</span><span class="sxs-lookup"><span data-stu-id="3c586-232">The following code returns all items from a table of **ToDoItems** sorted ascending by the *text* field.</span></span> <span data-ttu-id="3c586-233">*mToDoTable* is the reference to the backend table that you created previously:</span><span class="sxs-lookup"><span data-stu-id="3c586-233">*mToDoTable* is the reference to the backend table that you created previously:</span></span>

    mToDoTable.orderBy("text", QueryOrder.Ascending).execute().get();

<span data-ttu-id="3c586-234">The first parameter of the **orderBy** method is a string equal to the name of the field on which to sort.</span><span class="sxs-lookup"><span data-stu-id="3c586-234">The first parameter of the **orderBy** method is a string equal to the name of the field on which to sort.</span></span> <span data-ttu-id="3c586-235">The second parameter uses the **QueryOrder** enumeration to specify whether to sort ascending or descending.</span><span class="sxs-lookup"><span data-stu-id="3c586-235">The second parameter uses the **QueryOrder** enumeration to specify whether to sort ascending or descending.</span></span>  <span data-ttu-id="3c586-236">If you are filtering using the ***where*** method, the ***where*** method must be invoked before the ***orderBy*** method.</span><span class="sxs-lookup"><span data-stu-id="3c586-236">If you are filtering using the ***where*** method, the ***where*** method must be invoked before the ***orderBy*** method.</span></span>

### <a name="paging"></a><span data-ttu-id="3c586-237">How to: Return data in pages</span><span class="sxs-lookup"><span data-stu-id="3c586-237">How to: Return data in pages</span></span>
<span data-ttu-id="3c586-238">The first example shows how to select the top five items from a table.</span><span class="sxs-lookup"><span data-stu-id="3c586-238">The first example shows how to select the top five items from a table.</span></span> <span data-ttu-id="3c586-239">The query returns the items from a table of **ToDoItems**.</span><span class="sxs-lookup"><span data-stu-id="3c586-239">The query returns the items from a table of **ToDoItems**.</span></span> <span data-ttu-id="3c586-240">**mToDoTable** is the reference to the backend table that you created previously:</span><span class="sxs-lookup"><span data-stu-id="3c586-240">**mToDoTable** is the reference to the backend table that you created previously:</span></span>

    List<ToDoItem> result = mToDoTable.top(5).execute().get();


<span data-ttu-id="3c586-241">Here's a query that skips the first five items, and then returns the next five:</span><span class="sxs-lookup"><span data-stu-id="3c586-241">Here's a query that skips the first five items, and then returns the next five:</span></span>

    mToDoTable.skip(5).top(5).execute().get();

### <a name="selecting"></a><span data-ttu-id="3c586-242">How to: Select specific columns</span><span class="sxs-lookup"><span data-stu-id="3c586-242">How to: Select specific columns</span></span>
<span data-ttu-id="3c586-243">The following code illustrates how to return all items from a table of **ToDoItems**, but only displays the **complete** and **text** fields.</span><span class="sxs-lookup"><span data-stu-id="3c586-243">The following code illustrates how to return all items from a table of **ToDoItems**, but only displays the **complete** and **text** fields.</span></span> <span data-ttu-id="3c586-244">**mToDoTable** is the reference to the backend table that we created previously.</span><span class="sxs-lookup"><span data-stu-id="3c586-244">**mToDoTable** is the reference to the backend table that we created previously.</span></span>

    List<ToDoItemNarrow> result = mToDoTable.select("complete", "text").execute().get();

<span data-ttu-id="3c586-245">The parameters to the select function are the string names of the table's columns that you want to return.</span><span class="sxs-lookup"><span data-stu-id="3c586-245">The parameters to the select function are the string names of the table's columns that you want to return.</span></span>

<span data-ttu-id="3c586-246">The **select** method needs to follow methods like **where** and **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="3c586-246">The **select** method needs to follow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="3c586-247">It can be followed by paging methods like **top**.</span><span class="sxs-lookup"><span data-stu-id="3c586-247">It can be followed by paging methods like **top**.</span></span>

### <a name="chaining"></a><span data-ttu-id="3c586-248">How to: Concatenate query methods</span><span class="sxs-lookup"><span data-stu-id="3c586-248">How to: Concatenate query methods</span></span>
<span data-ttu-id="3c586-249">The methods used in querying backend tables can be concatenated.</span><span class="sxs-lookup"><span data-stu-id="3c586-249">The methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="3c586-250">Chaining query methods allows you to select specific columns of filtered rows that are sorted and paged.</span><span class="sxs-lookup"><span data-stu-id="3c586-250">Chaining query methods allows you to select specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="3c586-251">You can create complex logical filters.</span><span class="sxs-lookup"><span data-stu-id="3c586-251">You can create complex logical filters.</span></span>
<span data-ttu-id="3c586-252">Each query method returns a Query object.</span><span class="sxs-lookup"><span data-stu-id="3c586-252">Each query method returns a Query object.</span></span> <span data-ttu-id="3c586-253">To end the series of methods and actually run the query, call the **execute** method.</span><span class="sxs-lookup"><span data-stu-id="3c586-253">To end the series of methods and actually run the query, call the **execute** method.</span></span> <span data-ttu-id="3c586-254">For example:</span><span class="sxs-lookup"><span data-stu-id="3c586-254">For example:</span></span>

    mToDoTable.where()
        .year("due").eq(2013)
        .and().startsWith("text", "PRI0")
        .or().field("duration").gt(10)
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .top(20)
        .execute().get();

<span data-ttu-id="3c586-255">The chained query methods must be ordered as follows:</span><span class="sxs-lookup"><span data-stu-id="3c586-255">The chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="3c586-256">Filtering (**where**) methods.</span><span class="sxs-lookup"><span data-stu-id="3c586-256">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="3c586-257">Sorting (**orderBy**) methods.</span><span class="sxs-lookup"><span data-stu-id="3c586-257">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="3c586-258">Selection (**select**) methods.</span><span class="sxs-lookup"><span data-stu-id="3c586-258">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="3c586-259">paging (**skip** and **top**) methods.</span><span class="sxs-lookup"><span data-stu-id="3c586-259">paging (**skip** and **top**) methods.</span></span>

## <a name="inserting"></a><span data-ttu-id="3c586-260">How to: Insert data into the backend</span><span class="sxs-lookup"><span data-stu-id="3c586-260">How to: Insert data into the backend</span></span>
<span data-ttu-id="3c586-261">Instantiate an instance of the *ToDoItem* class and set its properties.</span><span class="sxs-lookup"><span data-stu-id="3c586-261">Instantiate an instance of the *ToDoItem* class and set its properties.</span></span>

    ToDoItem item = new ToDoItem();
    item.text = "Test Program";
    item.complete = false;

<span data-ttu-id="3c586-262">Then use **insert()** to insert an object:</span><span class="sxs-lookup"><span data-stu-id="3c586-262">Then use **insert()** to insert an object:</span></span>

    ToDoItem entity = mToDoTable.insert(item).get();

<span data-ttu-id="3c586-263">The returned entity matches the data inserted into the backend table, included the ID and any other values set on the backend.</span><span class="sxs-lookup"><span data-stu-id="3c586-263">The returned entity matches the data inserted into the backend table, included the ID and any other values set on the backend.</span></span>

<span data-ttu-id="3c586-264">Mobile Apps tables require a primary key column named **id**. By default, this column is a string.</span><span class="sxs-lookup"><span data-stu-id="3c586-264">Mobile Apps tables require a primary key column named **id**. By default, this column is a string.</span></span> <span data-ttu-id="3c586-265">The default value of the ID column is a GUID.</span><span class="sxs-lookup"><span data-stu-id="3c586-265">The default value of the ID column is a GUID.</span></span>  <span data-ttu-id="3c586-266">You can provide other unique values, such as email addresses or usernames.</span><span class="sxs-lookup"><span data-stu-id="3c586-266">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="3c586-267">When a string ID value is not provided for an inserted record, the backend generates a new GUID.</span><span class="sxs-lookup"><span data-stu-id="3c586-267">When a string ID value is not provided for an inserted record, the backend generates a new GUID.</span></span>

<span data-ttu-id="3c586-268">String ID values provide the following advantages:</span><span class="sxs-lookup"><span data-stu-id="3c586-268">String ID values provide the following advantages:</span></span>

* <span data-ttu-id="3c586-269">IDs can be generated without making a round trip to the database.</span><span class="sxs-lookup"><span data-stu-id="3c586-269">IDs can be generated without making a round trip to the database.</span></span>
* <span data-ttu-id="3c586-270">Records are easier to merge from different tables or databases.</span><span class="sxs-lookup"><span data-stu-id="3c586-270">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="3c586-271">ID values integrate better with an application's logic.</span><span class="sxs-lookup"><span data-stu-id="3c586-271">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="3c586-272">String ID values are **REQUIRED** for offline sync support.</span><span class="sxs-lookup"><span data-stu-id="3c586-272">String ID values are **REQUIRED** for offline sync support.</span></span>

## <a name="updating"></a><span data-ttu-id="3c586-273">How to: Update data in a mobile app</span><span class="sxs-lookup"><span data-stu-id="3c586-273">How to: Update data in a mobile app</span></span>
<span data-ttu-id="3c586-274">To update data in a table, pass the new object to the **update()** method.</span><span class="sxs-lookup"><span data-stu-id="3c586-274">To update data in a table, pass the new object to the **update()** method.</span></span>

    mToDoTable.update(item).get();

<span data-ttu-id="3c586-275">In this example, *item* is a reference to a row in the *ToDoItem* table, which has had some changes made to it.</span><span class="sxs-lookup"><span data-stu-id="3c586-275">In this example, *item* is a reference to a row in the *ToDoItem* table, which has had some changes made to it.</span></span>
<span data-ttu-id="3c586-276">The row with the same **id** is updated.</span><span class="sxs-lookup"><span data-stu-id="3c586-276">The row with the same **id** is updated.</span></span>

## <a name="deleting"></a><span data-ttu-id="3c586-277">How to: Delete data in a mobile app</span><span class="sxs-lookup"><span data-stu-id="3c586-277">How to: Delete data in a mobile app</span></span>
<span data-ttu-id="3c586-278">The following code shows how to delete data from a table by specifying the data object.</span><span class="sxs-lookup"><span data-stu-id="3c586-278">The following code shows how to delete data from a table by specifying the data object.</span></span>

    mToDoTable.delete(item);

<span data-ttu-id="3c586-279">You can also delete an item by specifying the **id** field of the row to delete.</span><span class="sxs-lookup"><span data-stu-id="3c586-279">You can also delete an item by specifying the **id** field of the row to delete.</span></span>

    String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
       mToDoTable.delete(myRowId);

## <a name="lookup"></a><span data-ttu-id="3c586-280">How to: Look up a specific item</span><span class="sxs-lookup"><span data-stu-id="3c586-280">How to: Look up a specific item</span></span>
<span data-ttu-id="3c586-281">Look up an item with a specific **id** field with the **lookUp()** method:</span><span class="sxs-lookup"><span data-stu-id="3c586-281">Look up an item with a specific **id** field with the **lookUp()** method:</span></span>

    ToDoItem result = mToDoTable
                        .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
                        .get();

## <a name="untyped"></a><span data-ttu-id="3c586-282">How to: Work with untyped data</span><span class="sxs-lookup"><span data-stu-id="3c586-282">How to: Work with untyped data</span></span>
<span data-ttu-id="3c586-283">The untyped programming model gives you exact control over JSON serialization.</span><span class="sxs-lookup"><span data-stu-id="3c586-283">The untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="3c586-284">There are some common scenarios where you may wish to use an untyped programming model.</span><span class="sxs-lookup"><span data-stu-id="3c586-284">There are some common scenarios where you may wish to use an untyped programming model.</span></span> <span data-ttu-id="3c586-285">For example, if your backend table contains many columns and you only need to reference a subset of the columns.</span><span class="sxs-lookup"><span data-stu-id="3c586-285">For example, if your backend table contains many columns and you only need to reference a subset of the columns.</span></span>  <span data-ttu-id="3c586-286">The typed model requires you to define all the mobile apps table's columns in your data class.</span><span class="sxs-lookup"><span data-stu-id="3c586-286">The typed model requires you to define all the mobile apps table's columns in your data class.</span></span>  

<span data-ttu-id="3c586-287">Most of the API calls for accessing data are similar to the typed programming calls.</span><span class="sxs-lookup"><span data-stu-id="3c586-287">Most of the API calls for accessing data are similar to the typed programming calls.</span></span> <span data-ttu-id="3c586-288">The main difference is that in the untyped model you invoke methods on the **MobileServiceJsonTable** object, instead of the **MobileServiceTable** object.</span><span class="sxs-lookup"><span data-stu-id="3c586-288">The main difference is that in the untyped model you invoke methods on the **MobileServiceJsonTable** object, instead of the **MobileServiceTable** object.</span></span>

### <a name="json_instance"></a><span data-ttu-id="3c586-289">How to: Create an instance of an untyped table</span><span class="sxs-lookup"><span data-stu-id="3c586-289">How to: Create an instance of an untyped table</span></span>
<span data-ttu-id="3c586-290">Similar to the typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span><span class="sxs-lookup"><span data-stu-id="3c586-290">Similar to the typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="3c586-291">Obtain the reference by calling the **getTable** method on an instance of the client:</span><span class="sxs-lookup"><span data-stu-id="3c586-291">Obtain the reference by calling the **getTable** method on an instance of the client:</span></span>

    private MobileServiceJsonTable mJsonToDoTable;
    //...
    mJsonToDoTable = mClient.getTable("ToDoItem");

<span data-ttu-id="3c586-292">Once you have created an instance of the **MobileServiceJsonTable**, it has virtually the same API available as with the typed programming model.</span><span class="sxs-lookup"><span data-stu-id="3c586-292">Once you have created an instance of the **MobileServiceJsonTable**, it has virtually the same API available as with the typed programming model.</span></span> <span data-ttu-id="3c586-293">In some cases, the methods take an untyped parameter instead of a typed parameter.</span><span class="sxs-lookup"><span data-stu-id="3c586-293">In some cases, the methods take an untyped parameter instead of a typed parameter.</span></span>

### <a name="json_insert"></a><span data-ttu-id="3c586-294">How to: Insert into an untyped table</span><span class="sxs-lookup"><span data-stu-id="3c586-294">How to: Insert into an untyped table</span></span>
<span data-ttu-id="3c586-295">The following code shows how to do an insert.</span><span class="sxs-lookup"><span data-stu-id="3c586-295">The following code shows how to do an insert.</span></span> <span data-ttu-id="3c586-296">The first step is to create a [JsonObject][1], which is part of the [gson][3] library.</span><span class="sxs-lookup"><span data-stu-id="3c586-296">The first step is to create a [JsonObject][1], which is part of the [gson][3] library.</span></span>

    JsonObject jsonItem = new JsonObject();
    jsonItem.addProperty("text", "Wake up");
    jsonItem.addProperty("complete", false);

<span data-ttu-id="3c586-297">Then, Use **insert()** to insert the untyped object into the table.</span><span class="sxs-lookup"><span data-stu-id="3c586-297">Then, Use **insert()** to insert the untyped object into the table.</span></span>

    mJsonToDoTable.insert(jsonItem).get();

<span data-ttu-id="3c586-298">If you need to get the ID of the inserted object, use the **getAsJsonPrimitive()** method.</span><span class="sxs-lookup"><span data-stu-id="3c586-298">If you need to get the ID of the inserted object, use the **getAsJsonPrimitive()** method.</span></span>

    jsonItem.getAsJsonPrimitive("id").getAsInt());

### <a name="json_delete"></a><span data-ttu-id="3c586-299">How to: Delete from an untyped table</span><span class="sxs-lookup"><span data-stu-id="3c586-299">How to: Delete from an untyped table</span></span>
<span data-ttu-id="3c586-300">The following code shows how to delete an instance, in this case, the same instance of a **JsonObject** that was created in the prior *insert* example.</span><span class="sxs-lookup"><span data-stu-id="3c586-300">The following code shows how to delete an instance, in this case, the same instance of a **JsonObject** that was created in the prior *insert* example.</span></span> <span data-ttu-id="3c586-301">The code is the same as with the typed case, but the method has a different signature since it references an **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="3c586-301">The code is the same as with the typed case, but the method has a different signature since it references an **JsonObject**.</span></span>

         mToDoTable.delete(jsonItem);

<span data-ttu-id="3c586-302">You can also delete an instance directly by using its ID:</span><span class="sxs-lookup"><span data-stu-id="3c586-302">You can also delete an instance directly by using its ID:</span></span>

         mToDoTable.delete(ID);

### <a name="json_get"></a><span data-ttu-id="3c586-303">How to: Return all rows from an untyped table</span><span class="sxs-lookup"><span data-stu-id="3c586-303">How to: Return all rows from an untyped table</span></span>
<span data-ttu-id="3c586-304">The following code shows how to retrieve an entire table.</span><span class="sxs-lookup"><span data-stu-id="3c586-304">The following code shows how to retrieve an entire table.</span></span> <span data-ttu-id="3c586-305">Since you are using a JSON Table, you can selectively retrieve only some of the table's columns.</span><span class="sxs-lookup"><span data-stu-id="3c586-305">Since you are using a JSON Table, you can selectively retrieve only some of the table's columns.</span></span>

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

<span data-ttu-id="3c586-306">The same set of filtering, filtering and paging methods that are available for the typed model are available for the untyped model as well.</span><span class="sxs-lookup"><span data-stu-id="3c586-306">The same set of filtering, filtering and paging methods that are available for the typed model are available for the untyped model as well.</span></span>

## <a name="custom-api"></a><span data-ttu-id="3c586-307">How to: Call a custom API</span><span class="sxs-lookup"><span data-stu-id="3c586-307">How to: Call a custom API</span></span>
<span data-ttu-id="3c586-308">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span><span class="sxs-lookup"><span data-stu-id="3c586-308">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="3c586-309">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span><span class="sxs-lookup"><span data-stu-id="3c586-309">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="3c586-310">From an Android client, you call the **invokeApi** method to call the custom API endpoint.</span><span class="sxs-lookup"><span data-stu-id="3c586-310">From an Android client, you call the **invokeApi** method to call the custom API endpoint.</span></span> <span data-ttu-id="3c586-311">The following example shows how to call an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="3c586-311">The following example shows how to call an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

    public void completeItem(View view) {

        ListenableFuture<MarkAllResult> result = mClient.invokeApi( "completeAll", MarkAllResult.class );

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

<span data-ttu-id="3c586-312">The **invokeApi** method is called on the client, which sends a POST request to the new custom API.</span><span class="sxs-lookup"><span data-stu-id="3c586-312">The **invokeApi** method is called on the client, which sends a POST request to the new custom API.</span></span> <span data-ttu-id="3c586-313">The result returned by the custom API is displayed in a message dialog, as are any errors.</span><span class="sxs-lookup"><span data-stu-id="3c586-313">The result returned by the custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="3c586-314">Other versions of **invokeApi** let you optionally send an object in the request body, specify the HTTP method, and send query parameters with the request.</span><span class="sxs-lookup"><span data-stu-id="3c586-314">Other versions of **invokeApi** let you optionally send an object in the request body, specify the HTTP method, and send query parameters with the request.</span></span> <span data-ttu-id="3c586-315">Untyped versions of **invokeApi** are provided as well.</span><span class="sxs-lookup"><span data-stu-id="3c586-315">Untyped versions of **invokeApi** are provided as well.</span></span>

## <a name="authentication"></a><span data-ttu-id="3c586-316">How to: add authentication to your app</span><span class="sxs-lookup"><span data-stu-id="3c586-316">How to: add authentication to your app</span></span>
<span data-ttu-id="3c586-317">Tutorials already describe in detail how to add these features.</span><span class="sxs-lookup"><span data-stu-id="3c586-317">Tutorials already describe in detail how to add these features.</span></span>

<span data-ttu-id="3c586-318">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using a variety of external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3c586-318">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using a variety of external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="3c586-319">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span><span class="sxs-lookup"><span data-stu-id="3c586-319">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="3c586-320">You can also use the identity of authenticated users to implement authorization rules in your backend.</span><span class="sxs-lookup"><span data-stu-id="3c586-320">You can also use the identity of authenticated users to implement authorization rules in your backend.</span></span>

<span data-ttu-id="3c586-321">Two authentication flows are supported: a **server** flow and a **client** flow.</span><span class="sxs-lookup"><span data-stu-id="3c586-321">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="3c586-322">The server flow provides the simplest authentication experience, as it relies on the identity providers web interface.</span><span class="sxs-lookup"><span data-stu-id="3c586-322">The server flow provides the simplest authentication experience, as it relies on the identity providers web interface.</span></span>  <span data-ttu-id="3c586-323">No additional SDKs are required to implement server flow authentication.</span><span class="sxs-lookup"><span data-stu-id="3c586-323">No additional SDKs are required to implement server flow authentication.</span></span> <span data-ttu-id="3c586-324">Server flow authentication does not provide a deep integration into the mobile device and is only recommended for proof of concept scenarios.</span><span class="sxs-lookup"><span data-stu-id="3c586-324">Server flow authentication does not provide a deep integration into the mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="3c586-325">The client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by the identity provider.</span><span class="sxs-lookup"><span data-stu-id="3c586-325">The client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by the identity provider.</span></span>  <span data-ttu-id="3c586-326">For example, you can integrate the Facebook SDK into your mobile application.</span><span class="sxs-lookup"><span data-stu-id="3c586-326">For example, you can integrate the Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="3c586-327">The mobile client swaps into the Facebook app and confirms your sign-on before swapping back to your mobile app.</span><span class="sxs-lookup"><span data-stu-id="3c586-327">The mobile client swaps into the Facebook app and confirms your sign-on before swapping back to your mobile app.</span></span>

<span data-ttu-id="3c586-328">Four steps are required to enable authentication in your app:</span><span class="sxs-lookup"><span data-stu-id="3c586-328">Four steps are required to enable authentication in your app:</span></span>

* <span data-ttu-id="3c586-329">Register your app for authentication with an identity provider.</span><span class="sxs-lookup"><span data-stu-id="3c586-329">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="3c586-330">Configure your App Service backend.</span><span class="sxs-lookup"><span data-stu-id="3c586-330">Configure your App Service backend.</span></span>
* <span data-ttu-id="3c586-331">Restrict table permissions to authenticated users only on the App Service backend.</span><span class="sxs-lookup"><span data-stu-id="3c586-331">Restrict table permissions to authenticated users only on the App Service backend.</span></span>
* <span data-ttu-id="3c586-332">Add authentication code to your app.</span><span class="sxs-lookup"><span data-stu-id="3c586-332">Add authentication code to your app.</span></span>

<span data-ttu-id="3c586-333">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span><span class="sxs-lookup"><span data-stu-id="3c586-333">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="3c586-334">You can also use the SID of an authenticated user to modify requests.</span><span class="sxs-lookup"><span data-stu-id="3c586-334">You can also use the SID of an authenticated user to modify requests.</span></span>  <span data-ttu-id="3c586-335">For more information, review [Get started with authentication] and the Server SDK HOWTO documentation.</span><span class="sxs-lookup"><span data-stu-id="3c586-335">For more information, review [Get started with authentication] and the Server SDK HOWTO documentation.</span></span>

### <a name="caching"></a><span data-ttu-id="3c586-336">How to: Add authentication code to your app</span><span class="sxs-lookup"><span data-stu-id="3c586-336">How to: Add authentication code to your app</span></span>
<span data-ttu-id="3c586-337">The following code starts a server flow login process using the Google provider:</span><span class="sxs-lookup"><span data-stu-id="3c586-337">The following code starts a server flow login process using the Google provider:</span></span>

    MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google);

<span data-ttu-id="3c586-338">Obtain the ID of the logged-in user from a **MobileServiceUser** using the **getUserId** method.</span><span class="sxs-lookup"><span data-stu-id="3c586-338">Obtain the ID of the logged-in user from a **MobileServiceUser** using the **getUserId** method.</span></span> <span data-ttu-id="3c586-339">For an example of how to use Futures to call the asynchronous login APIs, see [Get started with authentication].</span><span class="sxs-lookup"><span data-stu-id="3c586-339">For an example of how to use Futures to call the asynchronous login APIs, see [Get started with authentication].</span></span>

### <a name="caching"></a><span data-ttu-id="3c586-340">How to: Cache authentication tokens</span><span class="sxs-lookup"><span data-stu-id="3c586-340">How to: Cache authentication tokens</span></span>
<span data-ttu-id="3c586-341">Caching authentication tokens requires you to store the User ID and authentication token locally on the device.</span><span class="sxs-lookup"><span data-stu-id="3c586-341">Caching authentication tokens requires you to store the User ID and authentication token locally on the device.</span></span> <span data-ttu-id="3c586-342">The next time the app starts, you check the cache, and if these values are present, you can skip the log in procedure and rehydrate the client with this data.</span><span class="sxs-lookup"><span data-stu-id="3c586-342">The next time the app starts, you check the cache, and if these values are present, you can skip the log in procedure and rehydrate the client with this data.</span></span> <span data-ttu-id="3c586-343">However this data is sensitive, and it should be stored encrypted for safety in case the phone gets stolen.</span><span class="sxs-lookup"><span data-stu-id="3c586-343">However this data is sensitive, and it should be stored encrypted for safety in case the phone gets stolen.</span></span>

<span data-ttu-id="3c586-344">You can see a complete example of how to cache authentication tokens in [Cache authentication tokens section][7].</span><span class="sxs-lookup"><span data-stu-id="3c586-344">You can see a complete example of how to cache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="3c586-345">When you try to use an expired token, you receive a *401 unauthorized* response.</span><span class="sxs-lookup"><span data-stu-id="3c586-345">When you try to use an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="3c586-346">You can handle authentication errors using filters.</span><span class="sxs-lookup"><span data-stu-id="3c586-346">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="3c586-347">Filters intercept requests to the App Service backend.</span><span class="sxs-lookup"><span data-stu-id="3c586-347">Filters intercept requests to the App Service backend.</span></span> <span data-ttu-id="3c586-348">The filter code tests the response for a 401, triggers the sign-in process, and then resumes the request that generated the 401.</span><span class="sxs-lookup"><span data-stu-id="3c586-348">The filter code tests the response for a 401, triggers the sign-in process, and then resumes the request that generated the 401.</span></span>

## <a name="adal"></a><span data-ttu-id="3c586-349">How to: Authenticate users with the Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="3c586-349">How to: Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="3c586-350">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3c586-350">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="3c586-351">Using a client flow login is often preferable to using the `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span><span class="sxs-lookup"><span data-stu-id="3c586-351">Using a client flow login is often preferable to using the `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="3c586-352">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login](app-service-mobile-how-to-configure-active-directory-authentication.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="3c586-352">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login](app-service-mobile-how-to-configure-active-directory-authentication.md) tutorial.</span></span> <span data-ttu-id="3c586-353">Make sure to complete the optional step of registering a native client application.</span><span class="sxs-lookup"><span data-stu-id="3c586-353">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="3c586-354">Install ADAL by modifying your build.gradle file to include the following definitions:</span><span class="sxs-lookup"><span data-stu-id="3c586-354">Install ADAL by modifying your build.gradle file to include the following definitions:</span></span>

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

1. <span data-ttu-id="3c586-355">Add the following code to your application, making the following replacements:</span><span class="sxs-lookup"><span data-stu-id="3c586-355">Add the following code to your application, making the following replacements:</span></span>

* <span data-ttu-id="3c586-356">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span><span class="sxs-lookup"><span data-stu-id="3c586-356">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="3c586-357">The format should be https://login.windows.net/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="3c586-357">The format should be https://login.windows.net/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="3c586-358">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="3c586-358">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
* <span data-ttu-id="3c586-359">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span><span class="sxs-lookup"><span data-stu-id="3c586-359">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="3c586-360">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span><span class="sxs-lookup"><span data-stu-id="3c586-360">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
* <span data-ttu-id="3c586-361">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span><span class="sxs-lookup"><span data-stu-id="3c586-361">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
* <span data-ttu-id="3c586-362">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span><span class="sxs-lookup"><span data-stu-id="3c586-362">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="3c586-363">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="3c586-363">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

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

## <a name="how-to-add-push-notification-to-your-app"></a><span data-ttu-id="3c586-364">How to: add push notification to your app</span><span class="sxs-lookup"><span data-stu-id="3c586-364">How to: add push notification to your app</span></span>
<span data-ttu-id="3c586-365">You can [read an overview][6] that describes how Microsoft Azure Notification Hubs supports a wide variety of push notifications.</span><span class="sxs-lookup"><span data-stu-id="3c586-365">You can [read an overview][6] that describes how Microsoft Azure Notification Hubs supports a wide variety of push notifications.</span></span>  <span data-ttu-id="3c586-366">In [this tutorial][5], a push notification is sent to all devices every time a record is inserted.</span><span class="sxs-lookup"><span data-stu-id="3c586-366">In [this tutorial][5], a push notification is sent to all devices every time a record is inserted.</span></span>

## <a name="how-to-add-offline-sync-to-your-app"></a><span data-ttu-id="3c586-367">How to: add offline sync to your app</span><span class="sxs-lookup"><span data-stu-id="3c586-367">How to: add offline sync to your app</span></span>
<span data-ttu-id="3c586-368">The Quickstart tutorial contains code that implements offline sync. Look for code prefixed with comments:</span><span class="sxs-lookup"><span data-stu-id="3c586-368">The Quickstart tutorial contains code that implements offline sync. Look for code prefixed with comments:</span></span>

    // Offline Sync

<span data-ttu-id="3c586-369">By uncommenting the following lines of code you can implement offline sync, and you can add similar code to other Mobile Apps code.</span><span class="sxs-lookup"><span data-stu-id="3c586-369">By uncommenting the following lines of code you can implement offline sync, and you can add similar code to other Mobile Apps code.</span></span>

## <a name="customizing"></a><span data-ttu-id="3c586-370">How to: Customize the client</span><span class="sxs-lookup"><span data-stu-id="3c586-370">How to: Customize the client</span></span>
<span data-ttu-id="3c586-371">There are several ways for you to customize the default behavior of the client.</span><span class="sxs-lookup"><span data-stu-id="3c586-371">There are several ways for you to customize the default behavior of the client.</span></span>

### <a name="headers"></a><span data-ttu-id="3c586-372">How to: Customize request headers</span><span class="sxs-lookup"><span data-stu-id="3c586-372">How to: Customize request headers</span></span>
<span data-ttu-id="3c586-373">Configure a **ServiceFilter** to add a custom HTTP header to each request:</span><span class="sxs-lookup"><span data-stu-id="3c586-373">Configure a **ServiceFilter** to add a custom HTTP header to each request:</span></span>

    private class CustomHeaderFilter implements ServiceFilter {

        @Override
        public ListenableFuture<ServiceFilterResponse> handleRequest(
                    ServiceFilterRequest request,
                    NextServiceFilterCallback next) {

            runOnUiThread(new Runnable() {

                @Override
                public void run() {
                    request.addHeader("My-Header", "Value");                    }
            });

            SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
            try {
                ServiceFilterResponse response = next.onNext(request).get();
                result.set(response);
            } catch (Exception exc) {
                result.setException(exc);
            }
        }

### <a name="serialization"></a><span data-ttu-id="3c586-374">How to: Customize serialization</span><span class="sxs-lookup"><span data-stu-id="3c586-374">How to: Customize serialization</span></span>
<span data-ttu-id="3c586-375">The client assumes that the table names, column names, and data types on the backend all match exactly the data objects defined in the client.</span><span class="sxs-lookup"><span data-stu-id="3c586-375">The client assumes that the table names, column names, and data types on the backend all match exactly the data objects defined in the client.</span></span> <span data-ttu-id="3c586-376">There can be any number of reasons why the server and client names might not match.</span><span class="sxs-lookup"><span data-stu-id="3c586-376">There can be any number of reasons why the server and client names might not match.</span></span> <span data-ttu-id="3c586-377">In your scenario, you might want to do the following kinds of customizations:</span><span class="sxs-lookup"><span data-stu-id="3c586-377">In your scenario, you might want to do the following kinds of customizations:</span></span>

* <span data-ttu-id="3c586-378">The column names used in the App Service table don't match the names you are using in the client.</span><span class="sxs-lookup"><span data-stu-id="3c586-378">The column names used in the App Service table don't match the names you are using in the client.</span></span>
* <span data-ttu-id="3c586-379">Use an App Service table that has a different name than the class it maps to in the client.</span><span class="sxs-lookup"><span data-stu-id="3c586-379">Use an App Service table that has a different name than the class it maps to in the client.</span></span>
* <span data-ttu-id="3c586-380">Turn on automatic property capitalization.</span><span class="sxs-lookup"><span data-stu-id="3c586-380">Turn on automatic property capitalization.</span></span>
* <span data-ttu-id="3c586-381">Add complex properties to an object.</span><span class="sxs-lookup"><span data-stu-id="3c586-381">Add complex properties to an object.</span></span>

### <a name="columns"></a><span data-ttu-id="3c586-382">How to: Map different client and server names</span><span class="sxs-lookup"><span data-stu-id="3c586-382">How to: Map different client and server names</span></span>
<span data-ttu-id="3c586-383">Suppose that your Java client code uses standard Java-style names for the **ToDoItem** object properties, such as the following properties:</span><span class="sxs-lookup"><span data-stu-id="3c586-383">Suppose that your Java client code uses standard Java-style names for the **ToDoItem** object properties, such as the following properties:</span></span>

* <span data-ttu-id="3c586-384">mId</span><span class="sxs-lookup"><span data-stu-id="3c586-384">mId</span></span>
* <span data-ttu-id="3c586-385">mText</span><span class="sxs-lookup"><span data-stu-id="3c586-385">mText</span></span>
* <span data-ttu-id="3c586-386">mComplete</span><span class="sxs-lookup"><span data-stu-id="3c586-386">mComplete</span></span>
* <span data-ttu-id="3c586-387">mDuration</span><span class="sxs-lookup"><span data-stu-id="3c586-387">mDuration</span></span>

<span data-ttu-id="3c586-388">Serialize the client names into JSON names that match the column names of the **ToDoItem** table on the server.</span><span class="sxs-lookup"><span data-stu-id="3c586-388">Serialize the client names into JSON names that match the column names of the **ToDoItem** table on the server.</span></span> <span data-ttu-id="3c586-389">The following code uses the [gson][3] library to annotate the properties:</span><span class="sxs-lookup"><span data-stu-id="3c586-389">The following code uses the [gson][3] library to annotate the properties:</span></span>

    @com.google.gson.annotations.SerializedName("text")
    private String mText;

    @com.google.gson.annotations.SerializedName("id")
    private int mId;

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;

    @com.google.gson.annotations.SerializedName("duration")
    private String mDuration;

### <a name="table"></a><span data-ttu-id="3c586-390">How to: Map different table names between the client and the backend</span><span class="sxs-lookup"><span data-stu-id="3c586-390">How to: Map different table names between the client and the backend</span></span>
<span data-ttu-id="3c586-391">Map the client table name to a different mobile services table name by using an override of the [getTable()][4] method:</span><span class="sxs-lookup"><span data-stu-id="3c586-391">Map the client table name to a different mobile services table name by using an override of the [getTable()][4] method:</span></span>

    mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);

### <a name="conversions"></a><span data-ttu-id="3c586-392">How to: Automate column name mappings</span><span class="sxs-lookup"><span data-stu-id="3c586-392">How to: Automate column name mappings</span></span>
<span data-ttu-id="3c586-393">You can specify a conversion strategy that applies to every column by using the [gson][3] API.</span><span class="sxs-lookup"><span data-stu-id="3c586-393">You can specify a conversion strategy that applies to every column by using the [gson][3] API.</span></span> <span data-ttu-id="3c586-394">The Android client library uses [gson][3] behind the scenes to serialize Java objects to JSON data before the data is sent to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="3c586-394">The Android client library uses [gson][3] behind the scenes to serialize Java objects to JSON data before the data is sent to Azure App Service.</span></span>  <span data-ttu-id="3c586-395">The following code uses the **setFieldNamingStrategy()** method to set the strategy.</span><span class="sxs-lookup"><span data-stu-id="3c586-395">The following code uses the **setFieldNamingStrategy()** method to set the strategy.</span></span> <span data-ttu-id="3c586-396">This example will delete the initial character (an "m"), and then lower-case the next character, for every field name.</span><span class="sxs-lookup"><span data-stu-id="3c586-396">This example will delete the initial character (an "m"), and then lower-case the next character, for every field name.</span></span> <span data-ttu-id="3c586-397">For example, it would turn "mId" into "id."</span><span class="sxs-lookup"><span data-stu-id="3c586-397">For example, it would turn "mId" into "id."</span></span>

    client.setGsonBuilder(
        MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(new FieldNamingStrategy() {
            public String translateName(Field field) {
                String name = field.getName();
                return Character.toLowerCase(name.charAt(1))
                    + name.substring(2);
                }
            });

<span data-ttu-id="3c586-398">This code must be executed before using the **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="3c586-398">This code must be executed before using the **MobileServiceClient**.</span></span>

### <a name="complex"></a><span data-ttu-id="3c586-399">How to: Store an object or array property into a table</span><span class="sxs-lookup"><span data-stu-id="3c586-399">How to: Store an object or array property into a table</span></span>
<span data-ttu-id="3c586-400">So far, our serialization examples have involved primitive types such as integers and strings.</span><span class="sxs-lookup"><span data-stu-id="3c586-400">So far, our serialization examples have involved primitive types such as integers and strings.</span></span>  <span data-ttu-id="3c586-401">Primitive types easily serialize into JSON.</span><span class="sxs-lookup"><span data-stu-id="3c586-401">Primitive types easily serialize into JSON.</span></span>  <span data-ttu-id="3c586-402">If we want to add a complex object that doesn't automatically serialize to JSON, we need to provide the JSON serialization method.</span><span class="sxs-lookup"><span data-stu-id="3c586-402">If we want to add a complex object that doesn't automatically serialize to JSON, we need to provide the JSON serialization method.</span></span>  <span data-ttu-id="3c586-403">To see an example of how to provide custom JSON serialization, review the blog post [Customizing serialization using the gson library in the Mobile Services Android client][2].</span><span class="sxs-lookup"><span data-stu-id="3c586-403">To see an example of how to provide custom JSON serialization, review the blog post [Customizing serialization using the gson library in the Mobile Services Android client][2].</span></span>

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[How to: Create the Mobile Services client]: #create-client
[How to: Create a table reference]: #instantiating
[The API structure]: #api
[How to: Query data from a mobile service]: #querying
[Return all Items]: #showAll
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Concatenate query methods]: #chaining
[How to: Bind data to the user interface]: #binding
[How to: Define the layout]: #layout
[How to: Define the adapter]: #adapter
[How to: Use the adapter]: #use-adapter
[How to: Insert data into a mobile service]: #inserting
[How to: update data in a mobile service]: #updating
[How to: Delete data in a mobile service]: #deleting
[How to: Look up a specific item]: #lookup
[How to: Work with untyped data]: #untyped
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching
[How to: Handle errors]: #errors
[How to: Design unit tests]: #tests
[How to: Customize the client]: #customizing
[Customize request headers]: #headers
[Customize serialization]: #serialization
[Next Steps]: #next-steps
[Setup and Prerequisites]: #setup

<!-- Images. -->

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[Get started with authentication]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
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
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
