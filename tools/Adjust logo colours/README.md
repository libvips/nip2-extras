# Dependencies
* [nip2](https://github.com/libvips/nip2)
* Follow the [provided instructions](https://github.com/jpadfield/nip2-extras/blob/master/README.md) to add this new tool to [nip2](https://github.com/libvips/nip2). 

# Acknowledgement
* This function was created by @jpadfield
* The work was carried out as part of the general image processing development at [The National Gallery](https://www.nationalgallery.org.uk/)
<img src="https://github.com/jpadfield/nip2-extras/blob/master/graphics/NG Logo Black on Transparent 600.png" height="64" alt="IPERION-CH Logo">

# Summary
This function was written to quickly adjust the colours used in a 2 tone logo or text on a background colour. It was specifically created to allow multiple matching, simplified logos to be droped into "partner" pages on project websites.
* **INPUT:** The function takes in a single image.
* **OUTPUT:** The function will output a new version of the image with adjustable foreground and background colours.

# Instructions
* Open Nip2 software
* Ensure that you have added this new tool, given below onto a new or existing Toolkit.
* For this example the new tool "Adjust logo colours" was added to a new Toolkit called "TEST".
* In the main (workspace) window:
  * Open the existing logo image to be processed.
  * Select the image by left clicking on the alphanumeric tag tot he left of your image, this will be **A1** for the first image loaded into column **A**.
  * Run the new function **Toolkits > TEST > Adjust logo colours**.
  * This will create a new version of the image in your column with, as default, white image or text on a black brackground.
  * The forground and background colours can then be changed using the two provided colour widgets.
  
# Required Code
```
Adjust_logo_item = class
	Menuaction (_ "Adjust logo colours") 
		(_ "Alter the colours used in a 2 tone logo, text on a background colour") {
	action x = class
		_result {

		_vislevel = 3; 

		_bw_x = (colour_transform_to 1 x)?0;
		_sc_x = scale _bw_x;

		invert = Toggle "Swap Colours" false;
		
		colour_1 = Colour "sRGB" [0,0,0];
		colour_2 = Colour "sRGB" [255,255,255];

		_result = sub_action _sc_x colour_2 colour_1, invert 
					 = sub_action _sc_x colour_1 colour_2;
 
		sub_action a b c 
				= map_trinary process a b c
		{
			process a b c 
				= blend condition in1 in2
			{
				compare a b
					// prefer image as the condition
					= false, 
						!has_image a && has_image b
					// prefer mono images as the condition
					= false, 
						has_bands a && has_bands b && 
						get_bands a > 1 && get_bands b == 1
					// prefer uchar as the condition
					= false,
						has_format a && has_format b && 
						get_format a > Image_format.UCHAR && 
							get_format b == Image_format.UCHAR
					= true;
				args' = sortc compare [a, b, c];
				condition = args'?0;
				in1 = args'?1;
				in2 = args'?2;
			}
		}
		}
	}
```
