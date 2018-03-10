# Getting data off a pixel with a dead screen but USB debugging enabled
How to get data off your Google Pixel with a deadscreen but debugging enabled on your phone

note: I don't believe I needed to change the USB mode but if you do there's a handy link [here](https://android.stackexchange.com/questions/120026/how-do-i-change-from-ptp-to-mtp-mode-cannot-find-options-in-settings) on changing to MTP

Getting data from a Pixel with a broken screen but USB debugging enabled:

So assuming you've got USB debugging enabled on your phone you can easily do this using ADB. This is all done on macOS with ADB already installed.

1. Make sure your phone is on which is a bit of a hassle with a broken screen. You can hold down the power button to switch it off then hold it down to turn it back on.
2. Check to see if ADB recognises it by running `adb devices` If it recognises it there should be some ID listed under 'List of devices attached'. 

|List of devices attached|
|:----:|
|FA69F0491505	device|

3. `adb shell input text {your pin here}` e.g. `adb shell input text 1234`
4. `adb shell input keyevent 66` (this is the 'enter' key event)
5. `adb pull /storage/self/primary` . (this will pull all the data from /storage/self/primary to your current directory)
6. now if you run ls the new file will be visible. may not be visible inside finder so cd into the file and run open .

note: if you want to find a file that isn't /storage/self/primary then run adb shell and find the file you want. i used Android Studio's Android Device Monitor's File Explorer tab (Tools > Android > Android Device Monitor > File Explorer tab) to find the folder I needed which was DCIM. This can be useful since a few files are symbolic links which adb shell won't immediately tell you.
