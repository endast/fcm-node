fcm-node
========
A Node.JS simple interface to Google's Firebase Cloud Messaging (FCM). Supports both android and iOS, including topic messages

## Installation

Via [npm][1]:

    $ npm install fcm-node

## Usage

    var FCM = require('fcm-node');

    var serverKey = '';
    var fcm = new FCM(serverKey);

    var message = { //this may vary according to the message type (single recipient, multicast, topic, et cetera)
        to: 'registration_token', 
        collapse_key: 'your_collapse_key',
        
        notification: {
            title: 'Title of your push notification', 
            body: 'Body of your push notification' 
        },
        
        data: {  //you can send only notification or only data(or include both)
            my_key: 'my value',
            my_another_key: 'my another value'
        }
    };
    
    fcm.send(message, function(err, response){
        if (err) {
            console.log("Something has gone wrong!");
        } else {
            console.log("Successfully sent with response: ", response);
        }
    });


## Notes
* See [FCM documentation][2] for general details.
* See [Firebase Cloud Messaging HTTP Protocol][10] for details about the HTTP syntax used and JSON fields, notification and data objects. **(STRONGLY RECOMMENDED)**
* On **iOS**, set **content_available** when the app server needs to send a Send-to-Sync message. An inactive client app executes your logic in the background, while an app in the foreground passes the message to **didReceiveRemoteNotification**. (As seen in [FCM Docs][8])
* Some **iOS** users report a delay receiving the notifications and even a **'not receive at all'** scenario if the **priority** field is not set. This is due to a delivery policy with **APN** ([See APNs Provider API for a more detailed info][9])   

## Credits

Extended by [Leonardo Pereira][3].
Based on the great work on [fcm-push][7] by [Rasmunandar Rustam][4] cloned and modified from there, which in its turn, was cloned and modified from [Changshin Lee][5]'s [node-gcm][5]

## License

[GNU LESSER GENERAL PUBLIC LICENSE v3][6]

[1]: http://github.com/isaacs/npm
[2]: https://firebase.google.com/docs/cloud-messaging/server
[3]: mailto:jlcvp@cin.ufpe.br
[4]: mailto:nandar.rustam@gmail.com
[5]: https://github.com/h2soft/node-gcm
[6]: http://www.gnu.org/licenses/lgpl-3.0.txt
[7]: https://github.com/nandarustam/fcm-push
[8]: https://firebase.google.com/docs/cloud-messaging/concept-options
[9]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/APNsProviderAPI.html#//apple_ref/doc/uid/TP40008194-CH101-SW2
[10]: https://firebase.google.com/docs/cloud-messaging/http-server-ref

## Changelog
1.0.10 - \<FIX\> send function return only error object when multicast messages returned both error and success keys on response message  
1.0.9 - Updated Documentation <br />
1.0.8 - \<FIX\> 'icon' field no longer required in notification<br /> 
1.0.7 - renaming repository<br />
1.0.6 - bugfix: send function was always returning an error object for multicast messages (multiple registration ids)<br />
1.0.5 - bugfix with UTF-8 enconding and chunk-encoded transfers<br />
1.0.1 - forked from fcm-push and extended to accept topic messages without errors<br />
