iOS Cheatsheet
==============

A quick reference cheat sheet for iOS developers so that you turn coffee into code much faster:)

**Note**: The [Avocarrot](http://www.avocarrot.com/?utm_source=github&utm_medium=ios-cheatsheet) team will do its best to keep this cheatsheet updated but feel free to send your pull requests if you want to add a new entry or edit something.

##Contents

###Objective-C Basics

- [Classes](#classes)
- [Methods](#methods)
- [Operators](#operators)
- [Properties](#properties)
- [Constants](#constants)
- [Flow control statements](#flow-control-statements)
- [Delegates](#delegates)
- [Blocks](#blocks)

### Foundation Framework Classes

- [NSString](#nsstring)
- [NSArray](#nsarray)
- [NSDictionary](#nsdictionary)
- [Objective-C Literals](#objective-c-literals)

### C Related Code

- [Enumerated Types](#enumerated-types)


## Objective-C Basics

### Classes

#### Class header

```objc
@interface Human : NSObject

// Define properties and methods

@end
```

#### Class implementation

```objc
# import "Human.h"

@interface Human ()
// Define private properties and methods
@end

@implementation Human {
// Define private instance variables
}

// Provide method implementation code

@end
```

#### Creating an instance

```objc
Human * anObject = [[Human alloc] init];
```


### Methods

#### Defining methods

```objc
// Returns nothing and has no arguments
- (void)foo;

// Returns an NSString object and takes one argument of type NSObject
- (NSString *)fooWithArgument:(NSObject *)bar;

// Takes two arguments one of type NSObject and a second one of type NSString
- (void)fooWithArgument:(NSObject *)bar andArgument:(NSString *)baz;

// Defines a class method (note the + sign)
+ (void)aClassMethod;
```

#### Implementing methods

```objc
- (NSString *)fooWithArgument:(NSObject *)bar{
    // Do something here
    return retValue;
}
```

#### Calling a method

```objc
[anObject someMethod];
[anObject someMethodWithArg1:arg1 andArg2:arg2];
```


### Operators

#### Arithmetic Operators

Operator | Description
:---: | :---:
+ | Addition
- | Subtraction
* | Multiplication
/ | Division
% | Modulo

#### Comparison Operators

Operator | Description
:---: | :---:
x == y |    Returns true if x is equal to y
x > y | Returns true if x is greater than y
x >= y |    Returns true if x is greater than or equal to y
x < y | Returns true if x is less than y
x <= y |    Returns true if x is less than or equal to y
x != y |    Returns true if x is not equal to y


#### Logical Operators

Operator | Description
:---: | :---:
! | NOT
&& | Logical AND
&#124;&#124; | Logical OR

#### Compound Assignment Operators

Operator | Description
:---: | :---:
x += y |    Add x to y and place result in x
x -= y |    Subtract y from x and place result in x
x *= y |    Multiply x by y and place result in x
x /= y |    Divide x by y and place result in x
x %= y |    Perform Modulo on x and y and place result in x
x &= y |    Assign to x the result of logical AND operation on x and y
x |= y |    Assign to x the result of logical OR operation on x and y
x ^= y |    Assign to x the result of logical Exclusive OR on x and y

#### Bitwise Operators

Operator | Description
:---: | :---:
& | Bitwise AND
&#124; | Bitwise Inclusive OR
^ | Exclusive OR
~ | Bit inversion
<< | Shift Left
>> | Shift Right

#### Other operators

Operator | Description
:---: | :---:
() | Cast
? : | Ternary
& | Memory Address
* | Pointer


### Properties

#### Define properties

```objc
@property (attribute1, attribute2) NSString *aProperty;
```

Attribute Type | Purpose
:---: | ---
strong (iOS 4 = retain) (default)  | Creates an owning relationship to the object that is assigned to the property
weak  (iOS 4 = unsafe_unretained) | Creates a non-owning relationship
assign (default) | Normal assign, doesn’t perform any kind of memory-management
copy | Make an immutable copy of the object upon assignment
atomic (default) | Only allows one thread to access the property, which makes it threadsafe
nonatomic |  Allows multiple threads to access the property simultaneously, which makes it not threadsafe
readwrite (default) | Generates both getter and setter
readonly | Generates only getter
getter=method | Use this to specify a different name for the property's getter method
setter=method | Use this to specify a different name for the property's setter method

#### Access Properties

```objc
[anObject aProperty];

// Alternative
anObject.aProperty
```


### Constants

#### Preprocessing Macros

This is not an actual constant because it defines a macro which replaces all occurrences of ```MAX_NUMBER_OF_ITEMS``` with the actual value before compile time.

```objc
#define MAX_NUMBER_OF_ITEMS 10
```

#### Using const

A better approach is to use ```const```.
```objc
NSString *const kMyName = @"Clark";
```

#### Static and extern

If you know that the constant will only be available within it's implementation file, then you can use ```static```. Using ```static``` means that the constant will only be available in that file.

```objc
static NSString * const kMyName = @"Clark";
```

If you want to have a constant global then you should use extern.

```objc
// .h file
extern NSString * const kMyName;
```

```objc
// .m file
NSString * const kMyName = @"Clark";
```

### Flow control statements

#### If-else statement

```objc
if (someCondition) {
    // Execute if the condition is true
} else if (someOtherCondition) {
    // Execute if the other condition is true
} else {
    // Execute if the none of the above conditions are true
}
```

#### Ternary operator

```objc
someCondition ? @"True" : @"False";
```

#### For Loops

```objc
for (int i = 0; i < totalCount; i++) {
    // Do something here
}
```

#### While Loop

```objc
while (someCondition) {
   // Do something here
}
```

#### Do While Loop

```objc
do {
    // Do something here
} while (someCondition);
```

#### Switch

```objc
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


### Delegates

Delegates are a design pattern. A delegate allows one object to send messages to another object when an event happens. Check out [Apple docs](https:// developer.apple.com/library/ios/documentation/general/conceptual/CocoaEncyclopedia/DelegatesandDataSources/DelegatesandDataSources.html):

#### Become the delegate of a framework class

**Step 1**

Declare that your class adopts the protocol in the class definition in the angled brackets after the class/superclass name.

```objc
// MyTableViewController.h

@interface MyTableViewController : UIViewController <UITableViewDelegate, UITableViewDataSource>

@end
```

**Step 2**

Set your object as the delegate.

```objc
// MyTableViewController.m

[tableView setDelegate:self];

@end
```

**Step 3**

Implement the delegate methods.


#### Implement your own delegate for a custom class

**Step 1**

Declare the protocol methods

```objc
// Superman.h
#import <Foundation/Foundation.h>

@protocol SupermanDelegate <NSObject>

- (void)dodgeBullet;
- (void)seeThroughThings;
- (void)fly;

@optional
- (void)eat;

@end

@interface Superman : NSObject

// Create a property for the delegate reference
@property (nonatomic, weak) id <SupermanDelegate> delegate;

// Define other methods and properties

@end

```

**Step 2**

Set the delegate object

```objc
// Superman.m

[self setDelegate:anObject];
```

**Step 3**

Start sending delegate messages

```objc
// Superman.m

[self.delegate fly];
```

For the delegate methods that are optional, it is wise to check if the delegate can respond to that method before firing.

```objc
if ([self.delegate respondsToSelector:@selector(eat)]) {
  [self.delegate eat];
}
```

### Blocks

> Blocks are a language-level feature added to C, Objective-C and C++, which allow you to create distinct segments of code that can be passed around to methods or functions as if they were values.

For more information see [Programming with Objective-C - Working with Blocks](https:// developer.apple.com/library/ios/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/WorkingwithBlocks/WorkingwithBlocks.html)


**To declare a block local variable:**

```
returnType (^blockName)(parameterTypes) = ^returnType(parameters) {...};
```

**To declare a block property:**

```
@property (nonatomic, copy) returnType (^blockName)(parameterTypes);
```

**To accept a block as a method parameter:**

```
- (void)aMethodThatTakesABlock:(returnType (^)(parameterTypes))blockName;
```

**To pass a block as an argument in a method call:**

```
[someObject someMethodThatTakesABlock: ^returnType (parameters) {...}];
```

**To define a block type:**

```objc
typedef returnType (^TypeName)(parameterTypes);
TypeName blockName = ^returnType(parameters) {...};
```

## Class Specific

### NSString

#### Quick examples

```objc
NSString *firstName = @"Clark";
NSString *lastName = @"Kent";
NSString *fullName = [NSString stringWithFormat:  @"My full name is %@ %@",  firstName, lastName];
```

#### NSString format specifier

Specifier | Description
:---: | ---
%@  | Objective-C object
%zd | NSInteger
%lx, (long) | CFIndex
%tu | NSUInteger
%i  | int
%u  | unsigned int
%hi  | short
%hu  | unsigned short
%%  | Literal %


### NSArray

#### Quick examples

```objc
// Create an array
NSMutableArray *anArray = [@[@"Clark Kent", @"Lois Lane"] mutableCopy];

// Add new items
[anArray addObject:@"Lex Luthor"];

// Find array length
NSLog(@"Array has %d items", [anArray count]);

// Iterate over array items
for (NSString *person in anArray) {
 NSLog(@"Person: %@", person);
}

// Access item with index
NSString *superman = anArray[0];

// Remove Object @"Clark Kent"
[anArray removeObject:@"Clark Kent"];

// Remove the first Object
[anArray removeObjectAtIndex:0];
```

### NSDictionary

#### Quick examples

```objc
// Create a dictionary
NSMutableDictionary *person = [@{
                             @"firstname" : @"Clark",
                             @"lastname" : @"Kent",
                             @"age" : [NSNumber numberWithInt:35]
                             } mutableCopy];

// Access values
NSLog(@"Superman's first name is %@", person[@"firstname"]);
// or
NSLog(@"Superman's first name is %@", [person objectForKey:@"firstname"]);

// Find number of items in dictionary
[person count];

// Add an object to a dictionary
[person setObject:@"job" forKey:@"teacher"];

// Remove an object to a dictionary
[person removeObjectForKey:@"firstname"];
```

## Objective-C Literals

**Available from LLVM Compiler version 4.0 made available with Xcode 4.4**

### Strings
```objc
NSString *string = @"This is a string.";
```

### Numbers
```objc
NSNumber *number = @126;      // int          : Equal to [NSNumber numberWithInt:126];
NSNumber *number = @126u;     // unsigned int : Equal to [NSNumber numberWithUnsignedInt:126u];
NSNumber *number = @126l;     // long         : Equal to [NSNumber numberWithLong:126l];
NSNumber *number = @126.544f; // float        : Equal to [NSNumber numberWithFloat:126.544f]
NSNumber *number = @126.544;  // double       : Equal to [NSNumber numberWithDouble:126.544]
NSNumber *number = @YES;      // bool         : Equal to [NSNumber numberWithBool:YES]
```

### Containers
```objc
NSArray *array = @[object1,object2,object3]; // Creating NSArray
Object *object2 = array[1]; // Accessing NSArray
mutableArray[1] = newObject; // Adding to NSMutableArray

NSDictionary *dictionary = @{ @"key1" : object1, @"key2" : object2, @"key3" : object3 }; // Creating NSDictionary
Object *object2 = dictionary[@"key2"]; // Accessing NSDictionary
mutableDictionary[@"name"] = @"Henry"; // Adding to NSMutableDictionary
```

## C References

### Enumerated Types

#### Apple's Examples

Each enumerate is given a corresponding integer value, so

```objc
typedef NS_ENUM(NSInteger, UIButtonType) {
   UIButtonTypeCustom,
   UIButtonTypeSystem,
   UIButtonTypeDetailDisclosure,
   UIButtonTypeInfoLight,
   UIButtonTypeInfoDark,
   UIButtonTypeContactAdd,
   UIButtonTypeRoundedRect
};
```

is the same as

```objc
typedef NS_ENUM(NSInteger, UIButtonType) {
   UIButtonTypeCustom = 0,
   UIButtonTypeSystem = 1,
   UIButtonTypeDetailDisclosure = 2,
   UIButtonTypeInfoLight = 3,
   UIButtonTypeInfoDark = 4,
   UIButtonTypeContactAdd = 5,
   UIButtonTypeRoundedRect = 6
};
```

Explicitly defining the first enumerate's value is not required and it will default to 0.

#### Using an enumerated type

```objc
UIButton *button = [UIButton buttonWithType:UIButtonTypeInfoLight];
```

Or create a variable to pass into the methods like so...

```objc
UIButtonType myButtonType = UIButtonTypeCustom;
UIButton *myButton = [UIButton buttonWithType:myButtonType];
```

Because they are not objects, you must print enumerated types as integers

```objc
UIButtonType myButtonType = UIButtonTypeRoundedRect;

// Bad, will give you a warning and might even crash
NSLog(@"%@", myButtonType);

// Good, will properly print the value as an integer
NSLog(@"%d", myButtonType);
```
