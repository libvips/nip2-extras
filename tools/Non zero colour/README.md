# Dependencies
* [nip2](https://github.com/libvips/nip2)
* Follow the [provided instructions](https://github.com/jpadfield/nip2-extras/blob/master/README.md) to add this new tool to [nip2](https://github.com/libvips/nip2). 

# Acknowledgement
* This function was created by @jpadfield
* The work was carried out as part of the H2020 EU project [IPERION-CH](http://www.iperionch.eu/)
<img src="https://github.com/jpadfield/nip2-extras/blob/master/images/IPERION-CH_logo_trans.png" height="64" alt="IPERION-CH Logo">
<img src="https://github.com/jpadfield/nip2-extras/blob/master/images/iperion-ch-eu-tag_black.png" height="64" alt="IPERION-CH Grant Info">

# Summary
This function was written to calculate the non zero average colour of a given image. So it will discard all black or zero value pixels. The function was specifically created to calculate the average colour of slected areas of an image when the background non-selected area is all black or zero.
* **INPUT:** The function takes in a single image.
* **OUTPUT:** The function will output a simple colour widget, with a option to select the required colourspace, RGB, Lab, etc.

# Instructions
* Open Nip2 software
* Ensure that you have added this new tool, given below onto a new or existing Toolkit.
* For this example the new tool "Image to non zero colour" was added to a new Toolkit called "TEST".
* In the main (workspace) window:
  * Create or open an image to be processed.
  * Select the image by left clicking on the alphanumeric tag tot he left of your image, this will be **A1** for the first image loaded into column **A**.
  * Run the new function **Toolkits > TEST > Image to non zero colour**.
  
# Required Code
```
Non_zero_colour_item = class
 Menuaction (_ "Image to non zero colour") 
  (_ "Calculate the non zero average colour of an image") {
	  action x = class
		 _result {
		  _vislevel = 3; 
				
			_x = Colour_convert_item.sRGB_item.action x;
			_R = meanze _x?0;
			_G = meanze _x?1;
			_B = meanze _x?2; 
					
			_spaces = Image_type.image_colour_spaces;
			which = Option_enum (_ "Display") _spaces (_spaces.get_name 13);
			_rgb = Colour_to_colour_item.action [_R, _G, _B];
					
			_result = Colour_convert_item.conv which.value_thing _rgb;}}
```
