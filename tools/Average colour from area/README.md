# Dependeincies
* [nip2](https://github.com/libvips/nip2)
* Follow the [provide instructions](https://github.com/jpadfield/nip2-extras/blob/master/README.md) to add this new tool to [nip2](https://github.com/libvips/nip2). 

# Acknowledgement
* This function was created by @jpadfield
* The work was carried out as part of the H2020 EU project [IPERION-CH](http://www.iperionch.eu/)


# Summary
This function was written to calculate the non zero average colour of a given image. So it will discard all black or zero value pixels. The function was specifically created to calculate the average colour of slected areas of an image when the background non-selected area is all black or zero.
* **INPUT:** The function takes in a group of marks (or points).
* **OUTPUT:** The function will output a simple colour widget, with a option to select the required colourspace, RGB, Lab, etc.

# Instructions
* Open Nip2 software
* Ensure that you have added this new tool, given below onto a new or existing Toolkit.
* For this example the new tool "Average colour from area" was added to a new Toolkit called "TEST".
## In the main (workspace) window:
* Create or open an image.
  * Go to **File > Open** and select the image file.
  * or Drag and drop the file directly into the nip2 window.
* The image should appear as item (probably **A1**) in your currently selected column, showing a thumbnail along with some of the basic image metadata.
* Double click the thumbnail to open the **A1** image window.
## In the image window:
* Look at the image and determine which area you would like to select.
* Use the **ctrl + scroll wheel**, or the keyboard shortcuts (letters **I** & **O**), or the View menu on the window to zoom in/out of the image as required.
* Hold down **ctrl** and click to place a point on the image, it will appear as a cross with a numbered flag (probably A2) on the image.
* It will also be added to your currently selected column, back in the main window, underneath your image (probably A2).
* Repeat to place more points on your image to outline the shape of the polygon you wish to define. 
  * Points can be re-positioned by using the mouse to select and drag the numbered flags.
* Once you have created and positioned all of the required points close the image window.
## In the main (workspace) window:
* Select all the points by clicking ***A2*** to ***Ax***, where ***Ax*** is your last point, while holding down the **shift** key.
  * You can also select/deselect specific points, if required, by clicking on then while holding down the **ctrl** key.
* In the main menu options select **Edit > Group**.
* This will create a new group item in your selected column, which will contain a reference to all of the points you had selected.
* Select the group item, by clicking on it, and then in the main menu select **Toolkits > TEST > Average Colour from area**.
* Your average colour will then be added to your selected coloumn.
## Additional Notes 
The software continually recalculates the outcomes according to the changes you make, e.g. after following these steps, it is possible to go back and move the points on the **A1** image, and see an (almost) instant adjustment of the resulting colour.
* Replacing the image being used with another can be done by right clicking on images tag, say **A1**, and then selecting **Replace From File** from the menu provided.
* The set of points can then be re-positioned on the new image to define a different shape as required.
This way of working can save time - once the points are positioned the new averaged colour and Lab values appear without any further steps being necessary, provided that enough points are placed initially to allow the definition of a variety of irregular shapes.

# Required Code
```
Average_colour_from_group_of_marks_item = class
	Menuaction (_ "Average colour from area") 
		(_ "Calculate the non zero average colour of area defined by a Group of marks") {
			action x = class
				_result {
					_vislevel = 3; 
					
					_mask = select_polygon x;
					_oim = get_image ((x.value)?0);
					_im = if _mask then _oim else 0;
					_x = Colour_convert_item.sRGB_item.action _im;
					_R = meanze _x?0;
					_G = meanze _x?1;
					_B = meanze _x?2; 
					
					_spaces = Image_type.image_colour_spaces;
					which = Option_enum (_ "Display") _spaces (_spaces.get_name 13);
					_rgb = Colour_to_colour_item.action [_R, _G, _B];
					
					_result = Colour_convert_item.conv which.value_thing _rgb;}}
```
