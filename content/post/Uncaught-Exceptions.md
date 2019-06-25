---
title: "Debugging app terminating with uncaught exception of type NSException"
date: 2019-06-24T21:23:00+02:00
draft: false
slug: "debug-swift-uncaught-exceptions"
image: "images/steve-harvey-r4NMjZl19DY-unsplash.jpg"
tags: ["debug","swift","ios"]
comments: true     # set false to hide Disqus comments
share: true        # set false to share buttons
menu: ""           # set "main" to add this content to the main menu
---
Every now and then when working on the new features, our app crashes. Easy, peasy, right? Happens all the time. However sometimes **all** you can see is:
```
libc++abi.dylib: terminating with uncaught exception of type NSException
```
and then you wonder: Where did the stack trace go? The error message is not really helpful and asking lldb for more info using `expr $arg1` does not work. It may cause you to be stuck for a couple of hours, trying to pinpoint the cause of the exception. But how is this possible? Shouldn't debugger help you to track it down?!

Well, chances are, you brought this misery upon yourself. When iOS10 was introduced, the console output become overly verbose, so most of the people used **OS_ACTIVITY_MODE** environmental variable to silence all these noise. It works well, even a bit too well. Apparently this setting also disables the usual stack trace dump related to crashes.
Let's make it right again. Navigate to the Scheme settings by pressing `CMD <`(yes, that's `cmd`+`shift`+`,`), or by clicking your acitve scheme in the top left corner and choosing `Edit scheme`, then select `Run` and `Arguments` tab and **uncheck** the `OS_ACTIVITY_MODE = disable` box.
![](edit-scheme.png)

Now next time you launch your app, you'll get all the noise back, but also the helpful stack traces, like:
```
2019-06-18 14:46:34.608652+0200 XXX[16832:239956] *** Terminating app due to uncaught exception 'NSInvalidUnarchiveOperationException', reason: 'Could not instantiate class named IBNSLayoutConstraint because no class named IBNSLayoutConstraint was found; the class needs to be defined in source code or linked in from a library (ensure the class is part of the correct target)'
*** First throw call stack:
(
	0   CoreFoundation                      0x000000011b9936fb __exceptionPreprocess + 331
	1   libobjc.A.dylib                     0x000000011af37ac5 objc_exception_throw + 48
	2   CoreFoundation                      0x000000011b993555 +[NSException raise:format:] + 197
	3   UIFoundation                        0x0000000121ac06c9 UINibDecoderDecodeObjectForValue + 360
	4   UIFoundation                        0x0000000121ac0554 -[UINibDecoder decodeObjectForKey:] + 251
	5   UIKitCore                           0x00000001241b8b41 -[UIRuntimeConnection initWithCoder:] + 178
	6   UIFoundation                        0x0000000121ac0852 UINibDecoderDecodeObjectForValue + 753
	7   UIFoundation                        0x0000000121ac0af9 UINibDecoderDecodeObjectForValue + 1432
	8   UIFoundation                        0x0000000121ac0554 -[UINibDecoder decodeObjectForKey:] + 251
	9   UIKitCore                           0x00000001241b63f1 -[UINib instantiateWithOwner:options:] + 1216
	10  UIKitCore                           0x0000000123f333af -[UIViewController _loadViewFromNibNamed:bundle:] + 382
	11  UIKitCore                           0x0000000123f33d39 -[UIViewController loadView] + 177
	12  UIKitCore                           0x0000000123f34048 -[UIViewController loadViewIfRequired] + 172
	13  UIKitCore                           0x0000000123e98004 -[UINavigationController _updateScrollViewFromViewController:toViewController:] + 68
	14  UIKitCore                           0x0000000123e982f7 -[UINavigationController 
    ...
    ...
)
```
Don't forget to check the tick again once you are done. Otherwise you'll see all these `BoringSSL` message flood again;)

**Happy debugging!**

*//Photo by Steve Harvey on Unsplash*