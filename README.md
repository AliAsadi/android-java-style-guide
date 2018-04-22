# Android Java Style Guide

Follow a standard coding style in android, it will be easier for you and also for others to understand your code easily.

i encourage you to fork this guide and change the rules to fit your team's style guide.
Below, you may list some amendments to the style guide.

# #Naming

### Classes & Interfaces
Written in UpperCamelCase

BAD:
```java
interface onClickListener
```
GOOD:
```java
interface OnClickListener
```
---
### Methods 

Written in lowerCamelCase

BAD:
```java
public void SetValue(){
}
```
GOOD:
```java
public void setValue(){
}
```
---
### Fields

Written in lowerCamelCase.

```java
public int publicField;
```

* Non-public, non-static field names start with an m.
``` java
int mPackagePrivate;
private int mPrivate;
protected int mProtected;
```

* Static field names start with an s.
``` java
private static SingletonClass sSingleton;
```

* Static final fields should be written in uppercase, with an underscore separating words

```java
public static final int THE_ANSWER = 42;
```
---
### Variables & Parameters

Written in lowerCamelCase.

* Single character values to be avoided except for temporary looping variables.

BAD:
```java
public void setValue(){
  int i; 
  i = i+5;
}
```

GOOD:
```java
public void setValue(){
  for (int i =0 ;i < 10 ; i++)
}
```

----
### XML File Names

BAD:

```java
login.xml
intro_screen.xml
save_button.xml
```

GOOD:

``` java
activity_login.xml
fragment_intro_screen.xml
button_save.xml
```

----
### XML Attribute 

BAD:

``` java
 android:id="@+id/userName"
```

GOOD:

``` java
 android:id="@+id/user_name"
 android:id="@+id/name"
```

----
### Language

Use English spelling.

BAD:

``` java
String blak = "#00000";
String shahor = "#00000"; //hebrew
```

GOOD:

``` java
String black = "#00000";
```
----

### Treat acronyms as words

Treat acronyms and abbreviations as words in naming variables, methods, and classes to make names more readable:

BAD:
```java
XMLHTTPRequest
userID
class HTML
String URL
long ID
```

GOOD:
```java
XmlHttpRequest
userId
class Html	
String url	
long id	
```
---

# #Brace Style

Use standard brace style

BAD:

``` java
public Class
{
  private void setValue()
  {
  // do something ..
   }
}
```

GOOD:

``` java
public Class{
  private void setValue(){
  // do something ..
  }
}
```
* Conditional statements are always required to be enclosed with braces

BAD:
``` java
if (true) 
  setValue();
```

GOOD:
``` java
if (true){
  setValue();
 }
//OR
if (true)  setValue(); //acceptable
```
---
# #Declarations

### Access Level Modifiers
* methods and variables access level should be explicitly defined for classes

|Modifier       |   Class   |  Package  |  Subclass  |   World   |
| ---           |---        | ---       | ---        | ---       |
|`public `      |     Y     |     Y     |     Y      |     Y     |
|`protected`    |     Y     |     Y     |     Y      |     N     |
|`no modifier`  |     Y     |     Y     |     N      |     N     |
|`private`      |     Y     |     N     |     N      |     N     |

---
### Fields & Variables
single declaration per line

BAD:
```java
public String firstName,lastName,age;
```

GOOD:
```java
public String firstName;
public String lastName;
public String age;
```

---
# #Formatting & Spacing 

Code formatting is very important to make your code eaisly readable

* use the charm keyboard shorts to formate your code :

Windows : <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>L</kbd>

Mac : <kbd>⌘</kbd>+<kbd>Option</kbd>+<kbd>L</kbd>

----

# #Other 

### TODO comments

Use TODO comments for code that is temporary, a short-term solution, or good-enough but not perfect.

GOOD:

```java
// TODO: Remove this code after all production mixers understand.
// TODO: Change this to use a flag instead of a constant.
// TODO: Remove this code after the UrlTable has been checked in.

```

BAD:

```java
// TODO: Ali Esa Assadi (developer name)
// TODO: Ali - later
```

---
### Switch Statements

Switch cases should almost always have a default case.

1. To 'catch' an unexpected value

2. To handle 'default' actions, where the cases are for special behavior.

3. To show someone reading your code that you've covered that case.

BAD:

``` java
switch(type){
    case 1:
        //something
        break;
    case 2:
        //something else
         break;
}
```

GOOD:

``` java
switch(type){
    case 1:
        //something
         break;
    case 2:
        //something else
         break;
    default:
        // unknown type! should probably be some handling
         break;
}
```

---

### Annotations
Use standard Java annotations.
Android standard practices for the four predefined annotations in Java are:

```java
@Deprecated 
//Annotation type used to mark program elements that should no longer be used by programmers.
//Compilers produce a warning if a deprecated program element is used.
```

```java
@Override 
//Annotation type used to mark methods that override a method declaration in a superclass.
//Compilers produce an error if a method annotated with @Override does not actually override 
//a method in a superclass.
```

```java
@Nullable 
//Denotes that a parameter, field or method return value can be null.
```

```java
@NonNull 
//Denotes that a parameter, field or method return value can never be null.

```

---

### Exceptions

Don't ignore exceptions

Do not do this. While you may think your code will never encounter this error condition or that it is not important to handle it, 
ignoring exceptions as above creates mines in your code for someone else to trigger some day.


BAD:
```java
void setServerPort(String value) {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) { }
}
```


GOOD:

* if you are confident that ignoring the exception is appropriate then you may ignore it,
but you must also comment why with a good reason:

```java
/** If value is not a valid number, original port number is used. */
void setServerPort(String value) {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) {
        // Method is documented to just ignore invalid user input.
        // serverPort will just be unchanged.
    }
}
```

* Dangeros Throw a new RuntimeException
```java
/** Set port. If value is not a valid number, die. */

void setServerPort(String value) {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) {
        throw new RuntimeException("port " + value " is invalid, ", e);
    }
}
```

* Handle the error gracefully and substitute an appropriate value in the catch {} block.
 
```java
/** Set port. If value is not a valid number, 80 is substituted. */

void setServerPort(String value) {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) {
        serverPort = 80;  // default port for server
    }
}
```
* Throw a new exception that's appropriate to your level of abstraction.
```java
void setServerPort(String value) throws ConfigurationException {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) {
        throw new ConfigurationException("Port " + value + " is not valid.");
    }
}
```

* Throw the exception up to the caller of your method.
```java
void setServerPort(String value) throws NumberFormatException {
    serverPort = Integer.parseInt(value);
}
```
----

### Don't catch generic exception

It can also be tempting to be lazy when catching exceptions and do something like this:

BAD:

```java
try {
    someComplicatedIOFunction();        // may throw IOException
    someComplicatedParsingFunction();   // may throw ParsingException
    someComplicatedSecurityFunction();  // may throw SecurityException
    // phew, made it all the way
} catch (Exception e) {                 // I'll just catch all exceptions
    handleError();                      // with one generic handler!
}
```

GOOD:

Alternatives to catching generic Exception:

* Catch each exception separately as separate catch blocks after a single try.
 This can be awkward but is still preferable to catching all Exceptions.Beware repeating too much code in the catch blocks.

* Refactor your code to have more fine-grained error handling,
 with multiple try blocks. Split up the IO from the parsing, handle errors separately in each case.

* Rethrow the exception. Many times you don't need to catch the exception at this level anyway,
 just let the method throw it.

`Remember`: exceptions are your friend! When the compiler complains you're not catching an exception,
don't scowl. Smile: the compiler just made it easier for you to catch runtime problems in your code.

----

### Loop 

Loop variables should be declared in the for statement itself unless there is a compelling reason to do otherwise:

BAD:
```java
int i;
for (i = 0; i < n; i++) {
    doSomething(i);
}
```

GOOD:

```java
for (int i = 0; i < n; i++) {
    doSomething(i);
}
//OR
for (Iterator i = c.iterator(); i.hasNext(); ) {
    doSomethingElse(i.next());
}
```

# Inspiring

* [AOSP Java Code Style for Contributors](https://source.android.com/setup/contribute/code-style)

--------------------------------------------------------------------------------------------

**Feel free to submit any type of suggestions for improving the coding standard**

**Happy Coding!!!** ![](https://i.imgur.com/rneCZCN.png)

--------------------------------------------------------------------------------------------
