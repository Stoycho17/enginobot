---
weight: 1
title: Lesson 1
---

# Lesson 1

## Introduction

In Arduino, libraries are pre-written code modules that provide additional functionality to your projects. They contain functions and classes that can simplify complex tasks, such as working with sensors, displays, communication protocols, and more. In this lesson, you'll learn how to include libraries in your Arduino sketches to leverage their capabilities.


## Finding and Installing Libraries

```haskell
#include <LibraryName.h>
```

1. Start by opening the Arduino IDE on your computer.
2. Click on "Sketch" in the menu bar and select "Include Library" to open the Library Manager.
3. The Library Manager will show a list of libraries available for installation. You can browse the list or use the search bar to find a specific library.
4. Once you've found a library you want to install, click on it to select it.
5. Click the "Install" button to download and install the library.


## Including Libraries in Your Sketch

```haskell
#include <ginobot.h>
```

1. After installing a library, you need to include it in your Arduino sketch to use its functions and classes.
2. At the top of your sketch, before the void setup() function, add the #include directive followed by the library name in angle brackets (<>).


## Using Library Functions

```haskell
LibraryClass objectName;
objectName.functionName();
```

1. Once the library is included, you can start using its functions and classes in your sketch.
2. Refer to the library's documentation or examples to understand the available functions and classes and how to use them.
3. Create instances of classes defined in the library and call their member functions as needed.
