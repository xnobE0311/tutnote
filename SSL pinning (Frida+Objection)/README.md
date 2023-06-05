# Frida & objection android cert pin bypass (Linux)

The article talks about how to bypass cert pinning using frida server & objection script


# Requirement
Python version 3.10.x (dated 20230605)
Android SDK Platform-Tools
Frida server.
Objection
Target package app name (com.xxxx.yyy.zzz)

## Install Android SDK
Go to Android SDK Platform-Tools
[SDK Platform-Tools Release](https://developer.android.com/tools/releases/platform-tools)

1. In the is tutorial we will use Linux version, So download the Linux version
2. Extract the package to your expected location.
Noted: For the **adb** talking in this tutorial is located in folder "platform-tools" inside the package extracted location.
3. For any use of adb the following syntax is required
`./adb <option>`

## Frida-server
Install Frida-tools

Go "frida-core"'s release page in the below
[Frida-core Release page](https://github.com/frida/frida/releases)
Noted: you will be need frida-server-[x.y.z]-android-[cpu type].xz
1. Extract the file to your expected location.
2. In the extracted location, there should be a file named "frida-server-[x.y.z]-android-arm"
3. Rename the name at your convenient (internet common name: frida-server). I will name it "frida-server"
4. open adb shell with`./adb shell` in same directory with "frida-server"
Noted: If you connected multiple device you might need to use this command to find your device name`./adb devices`. You will need to use `./adb -s <device_name> shell` instead.
5. push the frida-server inside the location "/data/local/tmp/" with `./adb push frida-server /data/local/tmp`
6. Grant permission to "frida-server" with adb for execution with `./adb chmod 777 /data/local/tmp/frida-server"`
7. Run frida-server with `./frida-server` or run it without entering the directory by `./adb shell "/data/local/tmp/frida-server &"`

**Note:** for any permission error in adb should try to get super user with `su` in an root device. You will also need to grant superuser will android UI.

## Objection
1. Install Objection with pip
`pip install objection`
if any unsuccessful installation should also try 
`pip3` to install.
2. Build connection using frida-server before running objection.
3. Use the Objection with the following options to execute objection.
`objection com.xxxx.yyy.zzz explore -q` 
Noted if you are using root device as Frida note mentioned. You will need to use the following command:
`objection --gadget com.xxxx.yyy.zzz explore -q`
4. The command should execute the application.
5. To disable cert pinning you will need to use the following command
`android sslpinning disable`
6. Done!

## Frequent usage (after initial steps)
1. Plug the one device in your computer only and close all emulator.
2. save the adb location in a easy to find location. Open terminal there using UI Linux function
3. open adb along with frida-server with the following command `./adb shell"/data/local/tmp/frida-server &"` (& will keep the process run in background)
4. Run Objection with objection --gadget `com.xxxx.yyy.zzz explore -q`
5. Run cert pin kill script
`android sslpinning disable`

