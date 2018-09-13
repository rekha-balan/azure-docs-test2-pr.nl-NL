---
title: How to use Blob Storage from Xamarin | Microsoft Docs
description: The Azure Storage Client Library for Xamarin enables developers to create iOS, Android, and Windows Store apps with their native user interfaces. This tutorial shows how to use Xamarin to create an application that uses Azure Blob storage.
services: storage
documentationcenter: xamarin
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 44cb845d-cf78-4942-95b8-952da4f9a2c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 2ef27dc58e12d1b9e8eed54239332a53860ddd52
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553202"
---
# <a name="how-to-use-blob-storage-from-xamarin"></a><span data-ttu-id="d5d69-104">How to use Blob Storage from Xamarin</span><span class="sxs-lookup"><span data-stu-id="d5d69-104">How to use Blob Storage from Xamarin</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a><span data-ttu-id="d5d69-105">Overview</span><span class="sxs-lookup"><span data-stu-id="d5d69-105">Overview</span></span>
<span data-ttu-id="d5d69-106">Xamarin enables developers to use a shared C# codebase to create iOS, Android, and Windows Store apps with their native user interfaces.</span><span class="sxs-lookup"><span data-stu-id="d5d69-106">Xamarin enables developers to use a shared C# codebase to create iOS, Android, and Windows Store apps with their native user interfaces.</span></span> <span data-ttu-id="d5d69-107">This tutorial shows you how to use Azure Blob storage with a Xamarin application.</span><span class="sxs-lookup"><span data-stu-id="d5d69-107">This tutorial shows you how to use Azure Blob storage with a Xamarin application.</span></span> <span data-ttu-id="d5d69-108">If you'd like to learn more about Azure Storage, before diving into the code, see [Introduction to Microsoft Azure Storage](storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d5d69-108">If you'd like to learn more about Azure Storage, before diving into the code, see [Introduction to Microsoft Azure Storage](storage-introduction.md).</span></span>

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a><span data-ttu-id="d5d69-109">Create a new Xamarin Application</span><span class="sxs-lookup"><span data-stu-id="d5d69-109">Create a new Xamarin Application</span></span>
<span data-ttu-id="d5d69-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span><span class="sxs-lookup"><span data-stu-id="d5d69-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span></span> <span data-ttu-id="d5d69-111">This app will simply create a container and upload a blob into this container.</span><span class="sxs-lookup"><span data-stu-id="d5d69-111">This app will simply create a container and upload a blob into this container.</span></span> <span data-ttu-id="d5d69-112">We'll be using Visual Studio on Windows, but the same learnings can be applied when creating an app using Xamarin Studio on macOS.</span><span class="sxs-lookup"><span data-stu-id="d5d69-112">We'll be using Visual Studio on Windows, but the same learnings can be applied when creating an app using Xamarin Studio on macOS.</span></span>

<span data-ttu-id="d5d69-113">Follow these steps to create your application:</span><span class="sxs-lookup"><span data-stu-id="d5d69-113">Follow these steps to create your application:</span></span>

1. <span data-ttu-id="d5d69-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span><span class="sxs-lookup"><span data-stu-id="d5d69-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span></span>
2. <span data-ttu-id="d5d69-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span><span class="sxs-lookup"><span data-stu-id="d5d69-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span></span>
3. <span data-ttu-id="d5d69-116">Right-click your solution in the Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span><span class="sxs-lookup"><span data-stu-id="d5d69-116">Right-click your solution in the Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="d5d69-117">Search for **WindowsAzure.Storage** and install the latest stable version to all projects in your solution.</span><span class="sxs-lookup"><span data-stu-id="d5d69-117">Search for **WindowsAzure.Storage** and install the latest stable version to all projects in your solution.</span></span>
4. <span data-ttu-id="d5d69-118">Build and run your project.</span><span class="sxs-lookup"><span data-stu-id="d5d69-118">Build and run your project.</span></span>

<span data-ttu-id="d5d69-119">You should now have an application that allows you to click a button which increments a counter.</span><span class="sxs-lookup"><span data-stu-id="d5d69-119">You should now have an application that allows you to click a button which increments a counter.</span></span>

## <a name="create-container-and-upload-blob"></a><span data-ttu-id="d5d69-120">Create container and upload blob</span><span class="sxs-lookup"><span data-stu-id="d5d69-120">Create container and upload blob</span></span>
<span data-ttu-id="d5d69-121">Next, under your `(Portable)` project, you'll add some code to `MyClass.cs`.</span><span class="sxs-lookup"><span data-stu-id="d5d69-121">Next, under your `(Portable)` project, you'll add some code to `MyClass.cs`.</span></span> <span data-ttu-id="d5d69-122">This code creates a container and uploads a blob into this container.</span><span class="sxs-lookup"><span data-stu-id="d5d69-122">This code creates a container and uploads a blob into this container.</span></span> <span data-ttu-id="d5d69-123">`MyClass.cs` should look like the following:</span><span class="sxs-lookup"><span data-stu-id="d5d69-123">`MyClass.cs` should look like the following:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Threading.Tasks;

namespace XamarinApp
{
    public class MyClass
    {
        public MyClass ()
        {
        }

        public static async Task performBlobOperation()
        {
            // Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here");

            // Create the blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference to a previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create the container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference to a blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create the "myblob" blob with the text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

<span data-ttu-id="d5d69-124">Make sure to replace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span><span class="sxs-lookup"><span data-stu-id="d5d69-124">Make sure to replace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span></span> 

<span data-ttu-id="d5d69-125">Your iOS, Android, and Windows Phone projects all have references to your Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span><span class="sxs-lookup"><span data-stu-id="d5d69-125">Your iOS, Android, and Windows Phone projects all have references to your Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span></span> <span data-ttu-id="d5d69-126">You can now add the following line of code to each project to start taking advantage: `MyClass.performBlobOperation()`</span><span class="sxs-lookup"><span data-stu-id="d5d69-126">You can now add the following line of code to each project to start taking advantage: `MyClass.performBlobOperation()`</span></span>

### <a name="xamarinappdroid--mainactivitycs"></a><span data-ttu-id="d5d69-127">XamarinApp.Droid > MainActivity.cs</span><span class="sxs-lookup"><span data-stu-id="d5d69-127">XamarinApp.Droid > MainActivity.cs</span></span>

```csharp
using Android.App;
using Android.Widget;
using Android.OS;

namespace XamarinApp.Droid
{
    [Activity (Label = "XamarinApp.Droid", MainLauncher = true, Icon = "@drawable/icon")]
    public class MainActivity : Activity
    {
        int count = 1;

        protected override async void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from the "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from the layout resource,
            // and attach an event to it
            Button button = FindViewById<Button> (Resource.Id.myButton);

            button.Click += delegate {
                button.Text = string.Format ("{0} clicks!", count++);
            };

            await MyClass.performBlobOperation();
            }
        }
    }
}
```

### <a name="xamarinappios--viewcontrollercs"></a><span data-ttu-id="d5d69-128">XamarinApp.iOS > ViewController.cs</span><span class="sxs-lookup"><span data-stu-id="d5d69-128">XamarinApp.iOS > ViewController.cs</span></span>

```csharp
using System;
using UIKit;

namespace XamarinApp.iOS
{
    public partial class ViewController : UIViewController
    {
        int count = 1;

        public ViewController (IntPtr handle) : base (handle)
        {
        }

        public override async void ViewDidLoad ()
        {
            int count = 1;

            public ViewController (IntPtr handle) : base (handle)
            {
            }

            public override async void ViewDidLoad ()
            {
                base.ViewDidLoad ();
                // Perform any additional setup after loading the view, typically from a nib.
                Button.AccessibilityIdentifier = "myButton";
                Button.TouchUpInside += delegate {
                    var title = string.Format ("{0} clicks!", count++);
                    Button.SetTitle (title, UIControlState.Normal);
                };

                await MyClass.performBlobOperation();
            }

            public override void DidReceiveMemoryWarning ()
            {
                base.DidReceiveMemoryWarning ();
                // Release any cached data, images, etc that aren't in use.
            }
        }
    }
}
```

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a><span data-ttu-id="d5d69-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="d5d69-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span></span>

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated to within a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        int count = 1;

        public MainPage()
        {
            this.InitializeComponent();

            this.NavigationCacheMode = NavigationCacheMode.Required;
        }

        /// <summary>
        /// Invoked when this page is about to be displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used to configure the page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about to be displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used to configure the page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling the hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using the NavigationHelper provided by some templates,
                // this event is handled for you.
                Button.Click += delegate {
                    var title = string.Format("{0} clicks!", count++);
                    Button.Content = title;
                };

                await MyClass.performBlobOperation();
            }
        }
    }
}
```

## <a name="run-the-application"></a><span data-ttu-id="d5d69-130">Run the application</span><span class="sxs-lookup"><span data-stu-id="d5d69-130">Run the application</span></span>
<span data-ttu-id="d5d69-131">You can now run this application in an Android or Windows Phone emulator.</span><span class="sxs-lookup"><span data-stu-id="d5d69-131">You can now run this application in an Android or Windows Phone emulator.</span></span> <span data-ttu-id="d5d69-132">You can also run this application in an iOS emulator, but this will require a Mac.</span><span class="sxs-lookup"><span data-stu-id="d5d69-132">You can also run this application in an iOS emulator, but this will require a Mac.</span></span> <span data-ttu-id="d5d69-133">For specific instructions on how to do this, please read the documentation for [connecting Visual Studio to a Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span><span class="sxs-lookup"><span data-stu-id="d5d69-133">For specific instructions on how to do this, please read the documentation for [connecting Visual Studio to a Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span></span>

<span data-ttu-id="d5d69-134">Once you run your app, it will create the container `mycontainer` in your Storage account.</span><span class="sxs-lookup"><span data-stu-id="d5d69-134">Once you run your app, it will create the container `mycontainer` in your Storage account.</span></span> <span data-ttu-id="d5d69-135">It should contain the blob, `myblob`, which has the text, `Hello, world!`.</span><span class="sxs-lookup"><span data-stu-id="d5d69-135">It should contain the blob, `myblob`, which has the text, `Hello, world!`.</span></span> <span data-ttu-id="d5d69-136">You can verify this by using the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="d5d69-136">You can verify this by using the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5d69-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="d5d69-137">Next steps</span></span>
<span data-ttu-id="d5d69-138">In this tutorial, you learned how to create a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d5d69-138">In this tutorial, you learned how to create a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span></span> <span data-ttu-id="d5d69-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="d5d69-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span></span> <span data-ttu-id="d5d69-140">Please check out the following articles to learn more:</span><span class="sxs-lookup"><span data-stu-id="d5d69-140">Please check out the following articles to learn more:</span></span>

* [<span data-ttu-id="d5d69-141">Get started with Azure Blob Storage using .NET</span><span class="sxs-lookup"><span data-stu-id="d5d69-141">Get started with Azure Blob Storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="d5d69-142">Get started with Azure Table Storage using .NET</span><span class="sxs-lookup"><span data-stu-id="d5d69-142">Get started with Azure Table Storage using .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="d5d69-143">Get started with Azure Queue Storage using .NET</span><span class="sxs-lookup"><span data-stu-id="d5d69-143">Get started with Azure Queue Storage using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="d5d69-144">Get started with Azure File Storage on Windows</span><span class="sxs-lookup"><span data-stu-id="d5d69-144">Get started with Azure File Storage on Windows</span></span>](storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

