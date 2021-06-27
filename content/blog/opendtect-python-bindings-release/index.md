+++
title = "First Release of Python Bindings to OpendTect"
tags = ["python","opendtect"]
categories = ["Python"]
date = "2021-06-05"
draft = true
banner = "/blog/opendtect-python-bindings-release/image-01.png"
+++
The 6.6.8 release of the wmPlugins includes a Python module, **wmodpy**, to access OpendTect survey and well information. The **odpy**
module already included with OpendTect uses a C++ command line application to interact with the OpendTect data structures. Each
request for data by the **odpy** API incurs the overhead of starting this application and the writing and reading of the information as
an ascii data stream. The **wmodpy** module, however, is a direct binding to the OpendTect C++ code so Python is directly reading from
the in-memory representation of the data. Data access with the **wmodpy** module should be much faster.
<!--more-->

## Accessing the wmodpy Module
VS Code should be available in the package repositories of all the major Linux distributions so just install it like you would
any other application. Alternatively the [VS Code Download](https://code.visualstudio.com/Download) page provides a tar.gz download
for 64 bit Linux that can be copied into a users home folder for those situations where IT settings prevent a global software install.

For Windows go to the [VS Code Download](https://code.visualstudio.com/Download) page and download the package of choice. There are 3 options:
- User installer (software ends up in "C:\users\{username}\AppData\Local\Programs\Microsoft VS Code", recommended way)
- System installer (software ends up in "C:\Program Files", requires Administrator privileges)
- .zip (you unpack the zip file anywhere even on a usb stick)

Once installed, start it up (find the executable file call "code" in the application folder and run it from a console or click/double click
on it from your file manager/explorer) and add the following extensions:
- Python extension for Visual Studio Code
- Jupyter Extension for Visual Studio Code

## Survey Information Access
{{< figure src="image-01.png"  width="90%" class="img-centered" caption="**Displaying OpendTect survey locations in a VS Code Notebook**">}}

Open the OpendTect Python Settings dialog (Utilities|Installation|Python Settings menu)
{{< figure src="image-02.png"  width="90%" class="img-centered" caption="**OpendTect Python Settings Dialog**">}}

1.  For the Python IDE select "Other"
2.  Use the File Selector to locate the executable file called "code" in the VS Code application folder
3.  Use the icon button to set the location of an icon for the application (normally in the resources/app/resources/(linux|win32) subfolder
of the VS Code installation)
4.  Set a tooltip message, eg "VS Code"
5.  Press OK

This will add an icon to the OpendTect toolbar and a new menu item to the "Utilities|User Commands" menu to start Visual Studio Code. Starting
VS Code from within OpendTect ensures environment settings are compatible with the Python environment selected in the OpendTect Python
Settings dialog.

{{< figure src="image-03.png"  width="90%" class="img-centered" caption="**OpendTect After Adding VS Code**">}}
Click the icon or use the "Utilities|User Commands" menu to start a Visual Studio Code instance.

## Well Information Access
With these steps completed it should be possible to start VS Code from OpendTect and open a new blank Jupyter notebook by running
the Jupyter: Create Blank New Jupyter Notebook command from the VS Code Command Palette (Ctrl+Shift+P). This notebook will use
the Python environment selected in the OpendTect Python Settings dialog.
{{< figure src="image-04.png"  width="90%" class="img-centered" caption="**New Jupyter Notebook in VS Code**">}}

To find out more about using VS Code with Jupyter Notebooks check out the documentation:
-  [Working with Jupyter Notebooks in Visual Studio Code](https://code.visualstudio.com/docs/python/jupyter-support)
-  [Working with the Python Interactive window](https://code.visualstudio.com/docs/python/jupyter-support-py)



## What's Next
