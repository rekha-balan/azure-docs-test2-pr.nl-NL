
<span data-ttu-id="07c8b-101">The previous example contacts both the identity provider and the mobile service every time the app starts.</span><span class="sxs-lookup"><span data-stu-id="07c8b-101">The previous example contacts both the identity provider and the mobile service every time the app starts.</span></span> <span data-ttu-id="07c8b-102">Instead, you can cache the authorization token and try to use it first.</span><span class="sxs-lookup"><span data-stu-id="07c8b-102">Instead, you can cache the authorization token and try to use it first.</span></span>

* <span data-ttu-id="07c8b-103">The recommended way to encrypt and store authentication tokens on an iOS client is use the iOS Keychain.</span><span class="sxs-lookup"><span data-stu-id="07c8b-103">The recommended way to encrypt and store authentication tokens on an iOS client is use the iOS Keychain.</span></span> <span data-ttu-id="07c8b-104">We'll use [SSKeychain](https://github.com/soffes/sskeychain) -- a simple wrapper around the iOS Keychain.</span><span class="sxs-lookup"><span data-stu-id="07c8b-104">We'll use [SSKeychain](https://github.com/soffes/sskeychain) -- a simple wrapper around the iOS Keychain.</span></span> <span data-ttu-id="07c8b-105">Follow the instructions on the SSKeychain page and add it to your project.</span><span class="sxs-lookup"><span data-stu-id="07c8b-105">Follow the instructions on the SSKeychain page and add it to your project.</span></span> <span data-ttu-id="07c8b-106">Verify that the **Enable Modules** setting is enabled in the project's **Build Settings** (section **Apple LLVM - Languages - Modules**.)</span><span class="sxs-lookup"><span data-stu-id="07c8b-106">Verify that the **Enable Modules** setting is enabled in the project's **Build Settings** (section **Apple LLVM - Languages - Modules**.)</span></span>
* <span data-ttu-id="07c8b-107">Open **QSTodoListViewController.m** and add the following code:</span><span class="sxs-lookup"><span data-stu-id="07c8b-107">Open **QSTodoListViewController.m** and add the following code:</span></span>

```
        - (void) saveAuthInfo {
                [SSKeychain setPassword:self.todoService.client.currentUser.mobileServiceAuthenticationToken forService:@"AzureMobileServiceTutorial" account:self.todoService.client.currentUser.userId]
        }


        - (void)loadAuthInfo {
                NSString *userid = [[SSKeychain accountsForService:@"AzureMobileServiceTutorial"][0] valueForKey:@"acct"];
            if (userid) {
                NSLog(@"userid: %@", userid);
                self.todoService.client.currentUser = [[MSUser alloc] initWithUserId:userid];
                 self.todoService.client.currentUser.mobileServiceAuthenticationToken = [SSKeychain passwordForService:@"AzureMobileServiceTutorial" account:userid];

            }
        }
```

* <span data-ttu-id="07c8b-108">In `loginAndGetData`, modify  `loginWithProvider:controller:animated:completion:`'s completion block.</span><span class="sxs-lookup"><span data-stu-id="07c8b-108">In `loginAndGetData`, modify  `loginWithProvider:controller:animated:completion:`'s completion block.</span></span> <span data-ttu-id="07c8b-109">Add the following line right before `[self refresh]` to store the user ID and token properties:</span><span class="sxs-lookup"><span data-stu-id="07c8b-109">Add the following line right before `[self refresh]` to store the user ID and token properties:</span></span>

```
                [self saveAuthInfo];
```

* <span data-ttu-id="07c8b-110">Let's load the user ID and token when the app starts.</span><span class="sxs-lookup"><span data-stu-id="07c8b-110">Let's load the user ID and token when the app starts.</span></span> <span data-ttu-id="07c8b-111">In the `viewDidLoad` in **QSTodoListViewController.m**, add this right after`self.todoService` is initialized.</span><span class="sxs-lookup"><span data-stu-id="07c8b-111">In the `viewDidLoad` in **QSTodoListViewController.m**, add this right after`self.todoService` is initialized.</span></span>

```
                [self loadAuthInfo];
```
