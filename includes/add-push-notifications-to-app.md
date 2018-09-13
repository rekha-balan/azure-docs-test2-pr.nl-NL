
## <a id="add-push"></a><span data-ttu-id="fce95-101">Add Push Notifications to App</span><span class="sxs-lookup"><span data-stu-id="fce95-101">Add Push Notifications to App</span></span>
* <span data-ttu-id="fce95-102">In QSAppDelegate.m, import the iOS SDK and QSTodoService.h:</span><span class="sxs-lookup"><span data-stu-id="fce95-102">In QSAppDelegate.m, import the iOS SDK and QSTodoService.h:</span></span>

```
        #import <WindowsAzureMobileServices/WindowsAzureMobileServices.h>
        #import "QSTodoService.h"
```

* <span data-ttu-id="fce95-103">In `didFinishLaunchingWithOptions` in QSAppDelegate.m, insert the following lines right before `return YES;`:</span><span class="sxs-lookup"><span data-stu-id="fce95-103">In `didFinishLaunchingWithOptions` in QSAppDelegate.m, insert the following lines right before `return YES;`:</span></span>

```
        UIUserNotificationSettings* notificationSettings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeAlert | UIUserNotificationTypeBadge | UIUserNotificationTypeSound categories:nil];
        [[UIApplication sharedApplication] registerUserNotificationSettings:notificationSettings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
```

* <span data-ttu-id="fce95-104">In QSAppDelegate.m, add the following handler methods.</span><span class="sxs-lookup"><span data-stu-id="fce95-104">In QSAppDelegate.m, add the following handler methods.</span></span> <span data-ttu-id="fce95-105">Your app is now updated to support push notifications.</span><span class="sxs-lookup"><span data-stu-id="fce95-105">Your app is now updated to support push notifications.</span></span>

```
        // Registration with APNs is successful
        - (void)application:(UIApplication *)application
        didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {

            QSTodoService *todoService = [QSTodoService defaultService];
            MSClient *client = todoService.client;

            [client.push registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError *error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
            }];
        }

        // Handle any failure to register
        - (void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:
        (NSError *)error {
            NSLog(@"Failed to register for remote notifications: %@", error);
        }

        // Use userInfo in the payload to display a UIAlertView.
        - (void)application:(UIApplication *)application
              didReceiveRemoteNotification:(NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);

            NSDictionary *apsPayload = userInfo[@"aps"];
            NSString *alertString = apsPayload[@"alert"];

            UIAlertView *alert = [[UIAlertView alloc]
              initWithTitle:@"Notification"
              message:alertString
              delegate:nil
              cancelButtonTitle:@"OK"
              otherButtonTitles:nil];
            [alert show];
        }
```
