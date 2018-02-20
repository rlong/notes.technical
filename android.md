


Remote Debugging (including emulators)
======================================

* [Remote debugging with Android emulator - Stack Overflow](https://stackoverflow.com/questions/1754162/remote-debugging-with-android-emulator)

```
ssh -NL 5554:localhost:5554 -L 5555:localhost:5555 myuser@remote-server
killall adb
adb devices
```


