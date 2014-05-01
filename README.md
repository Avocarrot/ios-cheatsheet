iOS Cheatsheet
==============

A quick reference cheat sheet for iOS developers. 

**Note**: The [Avocarrot](http://www.avocarrot.com) team will do its best to keep this cheatsheet updated but feel to send your pull requests if you want to add a new entry or edit something.

##Contents
- Classes
- Methods
- Properties
- Constants
- NSString
- NSArray
- NSDictionary
- Flow control statements


###Classes

####Class header

```objC
@interface Human : NSObject

// Define properties and methds

@end
```

####Class implementation

```objC
#import "Human.h" 

@interface Human () 
// Define private properties and methods 
@end 
 
@implementation Human { 
// Define private instance variables 
} 
 
// Provide method implementation code 
 
@end 
```

####Creating an instance
```objC
Human * anObject = [[Human alloc] init];
```


###Methods

####Defining methods

```objC
// Returns nothing and has no arguments
- (void)foo;  

//Returns an NSString object and takes one argument of type NSObject 
- (NSSring *)fooWithArgument:(NSObject *)bar; 

//Takes two arguments one of type NSObject and a second one of type NSString 
- (void)fooWithArgument:(NSObject *)bar andArgument:(NSString *)baz; 

// Defines a class method (note the + sign)
+ (void)aClassMethod;
```  

####Implementing methods

```objC
- (NSSring *)fooWithArgument:(NSObject *)bar{
    //Do something here
    return retValue;
}
``` 

####Calling a method
```objC
[anObject someMethod];
[anObject someMethodWithArg1:arg1 andArg2:arg2];
``` 


###Properties

####Define properties
```objC
@property (attribute1, attribute2) NSString *aProperty;
```

Attribute Type | Purpose
:---: | ---
strong  | Ccreates an owning relationship to the object that is assigned to the property
weak | Creates a non-owning relationship 
assign | Normal assign, doesn’t perform any kind of memory-management
copy | Make an immutable copy of the object upon assignment. 
nonatomic |  Allows multiple threads to access the property simultaneously which makes it not threadsafe
readwrite  | Generates both getter and setter 
readonly | Generates only getter 
getter=method | Use this to specify a different name for the property's getter method.
setter=method | Use this to specify a different name for the property's setter method.

####Access Properties
```objC
[anObject aProperty];

//Alternative
anObject.aProperty
```


###Constants

####Preprocessing Macros
This is not an actual constant because it defines a macro which replaces all occurrences of ```MAX_NUMBER_OF_ITEMS``` with the actual value before compile time.
```objC
#define MAX_NUMBER_OF_ITEMS 10
```

####Using const
A better approach is to use ```const```.
```objC
NSString *const kMyName = @"George";
```

####Static and extern

If you know that the constant will only be available within it's implementation file, then you can use ```static```. Using ```static``` means that the constant will only be available in that file.
```objC
static NSString * const kMyName = @"George";
```

If you want to have a constant global then you should use extern. 
```objC
//.h file
extern NSString * const kMyName;
```

```objC
//.m file
NSString * const kMyName = @"George";
```

###NSString

####Quick examples
```objC
NSString *firstName = @"Clark"; 
NSString *lastName = @"Kent"; 
NSString *fullName = [NSString stringWithFormat:  @"My full name is %@ %@",  firstName, lastName]; 
```

####NSString format specifier

Specifier | Description
:---: | ---
%@  | Objective-C object
%lx, (long) | NSInteger, CFIndex
%lx, (unsigned long)  | NSUInteger
%i  | int
%u  | unsigned int
%hi  | short
%hu  | unsigned short
%%  | Literal %


###NSArray

####Quick examples
```objC
//Create an array
NSMutableArray *anArray = @[@"Clark Kent", @"Lois Lane"]; 

//Add new items
[anArray addObject:@"Lex Luthor"];

//Find array length
NSLog(@"Array has %d items", [anArray count]); 

//Iterate over array items
for (NSString *person in anArray) { 
 NSLog(@"Person: %@", person); 
} 

//Access item with index
NSString *superman = anArray[0];
```

###NSDictionary

####Quick examples
```objC
//Create a dictionary
NSDictionary *person = @{
    @"firstname" : @"Clark",
    @"lastname" : @"Kent",
    @"age" : [NSNumber numberWithInt:35]
};

//Access values 
NSLog(@"Superman's first name is %@", person[@"firstname"]);
//or
NSLog(@"Superman's first name is %@", [person objectForKey:@"firstname"]);
```


###Flow control statements

####If-else statement

```objC
if (someCondition) {
    // Execute if the condition is true
} else if (someOtherCondition) {
    // Execute if the other condition is true
} else {
    // Execute if the none of the above conditions are true
}
```

####Ternary operator

```objC
someCondition ? @"True" : @"False";
```

####For Loops

```objC
for (int i = 0; i < totalCount; i++) {
    // Do something here
}
```

####While Loop

```objC
while (someCondition) {
   // Do something here
}
```

####Do While Loop

```objC
do {
    // Do something here
} while (someCondition);
```

####Switch

```objC
switch (aLabel)
{
    case kLabelA:
        // Execute this if matched
        break;

     case kLabelB:
        // Execute this if matched
        break;

     default:
        // Execute this if matched
        break;
}
```