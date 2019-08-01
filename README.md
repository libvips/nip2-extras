# nip2-extras
[nip2](https://github.com/libvips/nip2) is a GUI for the [VIPS image processing library](https://libvips.github.io/libvips). This repository has been setup to share new functions and menu options for the nip2 software.

[nip2](https://github.com/libvips/nip2) is a very flexible piece of image processing software, all of its standard menu options from simple rotations to complex image based matrix manipulations are scripted as open and editable functions. These functions can be copied and edited or even linked together to created totally new options.

New [nip2](https://github.com/libvips/nip2) functions are created for lots of different individual reasons but can also often be useful for others so we will try to list them here.

# Documentation 
Please begin with the standard [nip2](https://github.com/libvips/nip2) [documentation](https://github.com/libvips/nip2#documentation) specific comments and documentation will be provided with each new function script.

# Dependencies
You will need [nip2](https://github.com/libvips/nip2) installed to make use of these scripts.

# Adding new nip2 functions
The Nip2 software is very flexible and can be enhanced with new tools to aid image processing activities. All of the existing menu options can be viewed and edited if required and new ones can be added as needed. New individual functions are refered to as **tools** and groups of these tools are refered to as **toolkits**.

To see or add to the current functions click on **Toolkits**, in the menu bar at the top of the nip2 window, and then **[Edit]** from the list of options.
## New Toolkits
* If this is the first tool you are adding please first create a new toolkit, if you have already done this you can skip down to adding a new tool.
* In the Toolkits window create a new toolkit, if required using the following menu options: **File > New > New Toolkit**
* You will be asked to provide a name for your new toolkit, type a new name in and then click **"Create"**.
* You will see that the name you typed in has been added to long list on the left of the Toolkits window.
## Adding a New Tool
* Select the Toolkit you would like to add your new tool to, by simply left clicking on the name of the Toolkit in the list on the left.
* To make sure you are ready to add a new tool select the option using the following menu options: **File > New > New Tool**
* Click the left mouse button in the blank section on the right of the Toolkits window.
* You can now either copy and paste the text for your new tool into the window, or directly write a new tool by typing in the required code.
* Once you are ready you can add the new tool to the list simply by selecting any of the other Toolkits in the list. 
  * This will make your tool accessable in your current nip2 window, but it has not saved your work.
  * If there is a problem with your code you will get an error message at this point.
* To save your new tool, re-select the Toolkit that you added it to and then save it using the following menu options: **File > Save Toolkit**.

# Moving new toolkits and tools when upgrading
All new toolkits and tools are saved locally on your computer in a specific **start** folder related to the current version of nip2. When you upgrade your software to a new version of nip2 these extra files are not automatically copied accross and you will need to do this manually.
* Please consult the nip2 documentation for the specific location of your **start** folder.
  * Linux: /home/USERNAME/.nip2-X.X.X/start
  * Windows: *TBC*
  * Mac: *TBC*
