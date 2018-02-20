


File
====

Deprecated
----------

```
__attribute__ ((deprecated))
__attribute__ ((deprecated)) // use CADataHelper & HLEntityHelper
```


Imports
-------


```
#import <Foundation/Foundation.h>
#import <UIKit/UIKit.h>
```



Classes
=======

Properties
----------

public property in the `.h` file:
```
@interface ZZZ

@property (strong, nonatomic) IBOutlet UIScrollView* categoriesScroll;

@end
```

private property in the `.m` file:
```
@interface ZZZ
@end

@implementation ZZZ {

HLTileController* _yyy;

}

@end
```

Pragma
------

```
#pragma mark - static members
#pragma mark - instance lifecycle
#pragma mark - static methods
#pragma mark - UI lifecycle
#pragma mark - overridden methods from super type
#pragma mark - UI/NIB callbacks
#pragma mark - <JBEntity> implementation
#pragma mark - <JBRequestHandler> implementation 
#pragma mark - <JBRequestHandler> implementation
#pragma mark - <JBJob> implementation
#pragma mark - <JBJobListener> implementation
#pragma mark - <NotificationListener> implementation
#pragma mark - <UIImagePickerControllerDelegate> implementation
#pragma mark - <UISearchDisplayDelegate> implementation
#pragma mark - <UITableViewDataSource> implementation
#pragma mark - <UITableViewDelegate> implementation
#pragma mark - <XPStackable> implementation 
#pragma mark - 
```

```
#pragma mark - <> implementation
```


Code Snippets
=============

class name from class
---------------------

```
NSStringFromClass([Configuration class])
```

Is an object an instance of a class
-----------------------------------


```
if( [notificationSource isKindOfClass:[ControlController class]] ) { 
```

Does a class implement a protocol
---------------------------------



```
// vvv http://stackoverflow.com/questions/2344672/objective-c-given-a-class-id-can-i-check-if-this-class-implements-a-certain-p

NSString *className; //assume this exists
Class class = NSClassFromString(className);
if ([class conformsToProtocol:@protocol(SomeProtocol)]) {
    id instance = [[class alloc] init];
    [instance create];
}

// ^^^ http://stackoverflow.com/questions/2344672/objective-c-given-a-class-id-can-i-check-if-this-class-implements-a-certain-p
```

responds to selector
--------------------

```
    if( [barButtonItem respondsToSelector:@selector(setTintColor:)] ) {
        
        UIColor* answer = [barButtonItem tintColor];
        [barButtonItem setTintColor:tintColor];
        return answer;
        
    }
```


singleton
---------


```
#import "CAMemoryModel.h"

static Type* _instance = nil; 

+ (void)initialize {
	
	_instance = [[Type alloc] init];
	
}

+(void)setInstance:(Type*)instance {

	if( nil != _instance ) {
		CARelease( _instance );
	}
	_instance = instance;
	CARetain(_instance); 

}
```

enumerate over a dictionary
---------------------------

```
    for( NSString* key in allHeaderFields ) {
        NSString* value = [allHeaderFields objectForKey:key];
    }
```







iOS: How to determine if a View associated with a ViewController visible
-------------------------------------------------------------------


### Option 1 ###

```
- (void)viewDidAppear:(BOOL)animated {

    Log_enteredMethod();
    [super viewDidAppear:animated];
    
    _viewIsVisible = true;
}

-(void)viewDidDisappear:(BOOL)animated {
    
    Log_enteredMethod();
    [super viewDidDisappear:animated];
    
    _viewIsVisible = false;
}

```

in init:

```
	answer->viewIsVisible = false;
```

### Option 2 ###


```
-(bool)isRunning {
    // vvv http://stackoverflow.com/questions/2777438/how-to-tell-if-uiviewcontrollers-view-is-visible
    
    
    if (self.isViewLoaded && self.view.window) {
        // viewController is visible
        return true;
    }
    
    // ^^^ http://stackoverflow.com/questions/2777438/how-to-tell-if-uiviewcontrollers-view-is-visible
    
    return false;
}
```


Threading / GCD
===============

Use Cocoa to invoke a method in the main thread
-----------------------------------------------


        [delegate performSelectorOnMainThread:@selector(playPauseJobCompletedWithStatus:) withObject:status waitUntilDone:NO];


GCD: Timed invocation of a block
--------------------------------


        dispatch_queue_t mainQueue = dispatch_get_main_queue();

dispatch_after(
	dispatch_time(DISPATCH_TIME_NOW, NSEC_PER_SEC*1),
	mainQueue(), 
	^(){

		Log_enteredMethod();
       });



GCD: Reference to `self`
------------------------


```
    __weak id weakSelf = self;

dispatch_async(dispatch_get_main_queue(), ^{
	if( !weakSelf ) { return; }
});

```


GCD: Invoke a method in the main thread
---------------------------------------


void (^block)(id someArg) = someBlock;
id object = someObject;
dispatch_async(dispatch_get_main_queue(), ^{
    block(someObject);
});


references: 
* http://stackoverflow.com/questions/7364169/how-to-dispatch-a-block-with-parameter-on-main-queue-or-thread



Preprocessor / `clang`
======================

Conditional inclusion based on platform
---------------------------------------


```
#import "TargetConditionals.h" 


#if TARGET_OS_IPHONE

#else

#endif
```


```
// works 
#if defined(__MAC_OS_X_VERSION_MIN_REQUIRED)
#endif


// MACOSX_DEPLOYMENT_TARGET does not seem to work :-(
#ifdef MACOSX_DEPLOYMENT_TARGET 
#endif


#ifdef IPHONEOS_DEPLOYMENT_TARGET
#endif

#if TARGET_OS_IPHONE
#import <MobileCoreServices/MobileCoreServices.h>
#else
#import <CoreServices/CoreServices.h>
#endif
```

http://developer.apple.com/library/ios/#documentation/DeveloperTools/Conceptual/cross_development/Configuring/configuring.html


Forward declare a class without importing it
------------------------------------------------

```
// in the .h file,declare the class … 
@class VLC; 
```




