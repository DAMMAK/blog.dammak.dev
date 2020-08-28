## How to run your flutter app on multiple emulator devices using vscode

Flutter is a cross-platform mobile framework i.e it support for both Android and iOS, developing flutter is so fascinating that you get to write once and run on both platform. in this post I will be showing how to run more than one emulator concurrently using Visual studio code, by default you can only run a single emulator at a time on a project. Thanks to super-fast hot reload and restart feature of flutter which makes development experience faster and better. But it would have been better if you can be testing/debugging your application as you are developing on both platforms devices without you have to wait for one device.

## Steps
- Create different emulator devices you want to run your application on. e.g iOS devices, Android device
NB: I won't be showing how to create emulator devices


 [How to create Android and iOS emulator device](https://grinchik.com/blog/how-to-install-ios-simulator-and-android-emulator-on-mac/) .


-  Make sure all the devices are launched.i.e all devices for iOS and Android.

-  Get ID for all your devices, to get the device id run ```flutter devices``` on your terminal to get your device id. [screenshot below]

![Screenshot 2020-05-10 at 7.18.03 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1589134834356/POTEo31RS.png)

-  Create a launch configuration setting for your flutter project. [screenshot below]

![Screenshot 2020-05-10 at 6.53.34 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1589137863580/x-TAbnlk_.png)

- Create a device profile for each of the devices in the launch.json

```
{
      "name": "iPad Pro",
      "request": "launch",
      "type": "dart",
      "deviceId": "CE96E50B-A047-40D9-9921-1359CA2CF231"

}

```

NB:
name is the profile name i.e device name although it can be any name. 
below is the sample configuration setting for my flutter app


```
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Flutter",
      "request": "launch",
      "type": "dart"
    },
    {
      "name": "Android",
      "request": "launch",
      "type": "dart",
      "deviceId": "emulator-5554"
    },
    {
      "name": "iPhone",
      "request": "launch",
      "type": "dart",
      "deviceId": "iPhone"
    },
    {
      "name": "iPad Pro",
      "request": "launch",
      "type": "dart",
      "deviceId": "CE96E50B-A047-40D9-9921-1359CA2CF231"
    }
  ],
  "compounds": [
    {
      "name": "All Devices",
      "configurations": ["Android", "iPhone", "iPad Pro"]
    }
  ]
}

```
- 
![Screenshot 2020-05-10 at 7.36.17 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1589135855993/Rhtru9sq2.png)



