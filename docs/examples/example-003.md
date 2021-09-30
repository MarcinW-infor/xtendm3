---
layout: default
title: Trigger Extension Example
parent: Examples
nav_order: 1
---

# Trigger Extension Example
{: .no_toc }

Working with Trigger Extension in XtendM3
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Description
Trigger Extension is a simple type of extension, that consists in the execution of certain procedures in the designed extension, at the designated moment of program operation. It needs an extension point, at which it will be executed and triggerred by M3. It is used to modify orextend M3 Business Logic. Trigger extension can use a lot of useful API, which have various uses depending on the user's needs.


## Use cases
* Expanding the programme's functionality
* Modifications to the operations at a given extension point
* Allows implementation of functionality without changing the M3 itself at the source code


## Important Note
Always test the examples for your own solution before using them in production.

## Step by step implementation
### 1. Create new extension button
After opening the main window with the access to M3, it is needed to enter the Administration Tools section inside the table on the left side of the screen. After that select XtendM3.
<br>
//SCREEN1
<br>
To create new extension it is needed to use the "Create new extension button" as shown on the screen below:
<br>
//SCREEN2
<br>
### 2. Extension Type as a trigger extension - executed by a trigger
Opened window displays an option to select the type of extension to be designed. Select "Trigger" as described "Executed by a trigger" and then click next.
<br>
//SCREEN3
<br>
### 3. Complete all inputs + description of them
The next window will require to fill in some data:
- Name of the extension
- Program name where to implement designed extension
After clicking "Next" button, another options will be displayed
- Method of the executed extension point
- Advice for the extension method
<br>
SCREEN4
<br>
Depending on the selected programe, all sorts of methods can be available in the place for the selected method from modifying access to programmes data to interactively designed messages depending on the event at the extension point
The example presents udage of interactive pop up window extension inside the program. It is needed to choose the PEINZ from the method panel. MEthod PEINZ means initialization of designed event at the E panel:
- P as the panel word 
- E as the name of the Panel
- INZ as the initialization 
There are also several methods similar to PEINZ like PEUPD or PECHK. All vary according to the type of method and the panel on which the extension point occurs. All available methods depend on the selected programme.
The last box describes usage of selected method. It asks if the extension point should be before "PRE" or after "POST" selected method.
<br>
SCREEN5
<br>
After inputting all necessary data click create button
New extension is created. Now it is time to implement the functionality of the new extension.

### 4. Skeleton of the extension
The skeleton of the basic extension is empty. It is only made extended by the ExtendM3Trigger. Here is the place to implement the new extension.
<br>
SCREEN6
<br>
Over the code field there are several tools with which you can operate on the designed extension
<br>
SCREEN7
<br>
Listing them from the left side they are used to:
- enable editing mode
- export the code
- extra settings to change the parameters of the extension or enable it etc.
- delete the extension
- information about the extension'
- test compile
- refresh

### 5. Examples of trigger extension and usage of APIs
To start working with code of the new extension, the first thing to do is to enable edit mode. After that it is possible to implement the designed functionality
It is recommended to implement designed for XtendM3 APIs to exploit the full potential of the extension. Several APIs are described in the documentation at the [link](https://infor-cloud.github.io/xtendm3/docs/documentation/api-specification) 
In the first example the [ProgramAPI](https://infor-cloud.github.io/xtendm3/docs/documentation/api-specification/program-api/) and the [InteractiveAPI](https://infor-cloud.github.io/xtendm3/docs/documentation/api-specification/interactive-api/) are used to create a pop up message with the welcome text and the information about running program.
To implement these APIs it is needed just to include them as new objects inside the constructor of the extension and implement all the designed functionality of it inside the main() method as at below screen:
<br>
SCREEN8
<br>
After implementing functionality it is needed to save the extension. If it is written correctly there should be a message with the proper information with success. In case of error, the appropriate error message will appear and the implementation will not be saved until the error is resolved. After saving an extension it is a good practice to use a test compilation of the program just to check if everything is working properly.

### 6. Activation, Funcionality and description of designed extension
The next step is to activate the extension. It can be activated inside the settings panel of the extension. To activate the extension, the activate slider needs to be turned on. 
<br>
SCREEN9
<br>
After that it is possible to run the program with activated extension by using CTRL+R key combination and inputting the name of the program. While the program is running, the new implemented extension can be tested by the user. In this example the message is popped up on the panel E after execution of the extension method.
<br>
SCREEN10
<br>


### 7. Important notes
- It is a good practice to use a test compilation of the program just to check if everything is working properly.
- The convergence of the presented data is entirely coincidental.


## Extension Code
Here's an overview of the designed extensions, the exported files can be downloaded and imported in your own environments.

```groovy
public class test extends ExtendM3Trigger {
  private final InteractiveAPI interactive;
  private final ProgramAPI program;
  
  public test(InteractiveAPI interactive, ProgramAPI program) {
    this.interactive = interactive;
    this.program = program;
  }
  
  public void main() {
    interactive.showOkDialog("Hello XtendM3 user! You are using ${program.getProgramName()} program.");
  }
}
```

### Exported Extension
- [NumberUtil.json](https://infor-cloud.github.io/xtendm3/assets/attachments/ex001/DateUtil.json)

### See Also
N/A