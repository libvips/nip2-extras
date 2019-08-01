# Dependencies
* [nip2](https://github.com/libvips/nip2)
* Follow the [provided instructions](https://github.com/jpadfield/nip2-extras/blob/master/README.md) to add this new tool to [nip2](https://github.com/libvips/nip2). 

# Acknowledgement
* This function was created by @jpadfield
* The work was carried out as part of the H2020 EU project [IPERION-CH](http://www.iperionch.eu/)
<img src="https://github.com/jpadfield/nip2-extras/blob/master/graphics/IPERION-CH_logo_trans.png" height="64" alt="IPERION-CH Logo">
<img src="https://github.com/jpadfield/nip2-extras/blob/master/graphics/iperion-ch-eu-tag_black.png" height="64" alt="IPERION-CH Grant Info">

# Summary
This function was written to simplify the process of adding consistent scale bars to sets of images in preparation for publication. The initial use was collecting a set of microscope images of know resolution and then adding a scale bar to them all at once.
* **INPUT:** The function requires and image and a number (the resolution scale in ppmm)
* The function can also be run on a group of images and a single resolution value or a matching group of individual resolution numbers.
* **OUTPUT:** The function will output an image or groups of images annotated with the required scale bar. A series of options are provided as part of the output to control the colour, position, thickness and size, etc. of the scale bar.

# Instructions
* Open Nip2 software
* Ensure that you have added this new tool, given below onto a new or existing Toolkit.
* For this example the new tool "Draw Scale Bar" was added to a new Toolkit called "TEST".
## In the main (workspace) window:
* Create or open an image.
  * Go to **File > Open** and select the image or group of images required.
* The image or group should appear as item (probably **A1**) in your currently selected column, showing a thumbnail along with some of the basic image metadata.
* If using a single resolution value in ppmm, simply type that number into the text box at the bottom of your column.
  * A group of resolution numbers can also be created by typing in the values, in the same text box, using the syntax shown:
```
Group [10000,15000,20000]
```
* Select your image/group of images, by clicking on it, and then also select your resolution number of group of resolution numbers by clicking on it while holding down the **ctrl** key.
* In the main menu select **Toolkits > TEST > Draw Scale Bar**.
* A new scale bar widget will be added to you selected column.
* Adjust the various options as required to adjust the format of the scale bar.
  * For single images the results will be shown in the thumbnail of the widget.
  * For groups of images you will need use the **Edit > Ungroup** option to unpack the group and see all of the results.
  * Please note that groups can be saved in one go.



# Required Code
```
Draw_scalebar_item = class 
	Menuaction (_"Draw Scale Bar")
		( "Add a consistant scale bar to an image (x), or a group of images, based on a defined resolution (y) (ppmm)") {
		action x y = class
		_result {
			_vislevel = 3;

			ow = Option "Output Width" ["One Column", "Two Column", "Custom (cm)"] 1;
			cow = Expression "Optional Custom Output Width (cm)" 8;			
			text = Option "Display Text" [
				"20 µm", "50 µm", "100 µm", "200 µm", "500 µm", 
				"1 mm", "2 mm", "5 mm", "1 cm", "2 cm", "5 cm", 
				"10 cm", "20 cm", "50 cm", "1 m"] 1;			
			pos = Option "Position Text" ["Left", "Right"] 0;
			col = Option "Text Colour" ["White", "Black", "Red"] 0;

			Options = class
				{
				_vislevel = 1;
				dpi = Expression "Output Printing DPI" 600;
				ed = Expression "Distance from printed side edge ( % of printed width )" 4;
				bd = Expression "Distance from printed bottom edge (  % of printed height )" 3;
				thick = Scale "Line thickness" 1 50 5;
				font = Fontname "Use font" Workspaces.Preferences.PAINTBOX_FONT;
				}

			_ow' = [80, 160, (cow.expr*10)]?ow;
			_sbw = [0.02, 0.05, 0.1, 0.2, 0.5, 1, 2, 5, 10, 20, 50, 100, 200, 500, 1000]?text;
			_colv = [[255, 255, 255], [0, 0, 0], [255, 0, 0]];
			_col' = 	Colour "sRGB" _colv?col;
			_dpi = Options.dpi.expr;
			_dpmm = _dpi/(2.54*10);
			_pw =_ow' * _dpmm;
			_edmm = (Options.ed.expr * _ow')/100;
			_interp = Interpolate_picker Interpolate_type.BILINEAR;
      
			//Check for a group + int pair
			_y = y, is_Group y;
			   = Group (map (const y) [1..(len x.value)]), is_Group x;
			   = y;

      		_result
				= map_binary process x _y
        		{
				process im ppmm = blend (Image scale) ink' nim        
						{
            			// make an ink compatible with the image
            			ink' = colour_transform_to (get_type im) _col';
						im_scale = _pw / im.width;
						ph = im.height * im_scale;
						oh = (_ow' * im.height)/im.width;
						
						nim = resize _interp im_scale im_scale im;
						nppmm = ppmm * im_scale;
						
			          w = _sbw * nppmm;
						bdmm = (Options.bd.expr * oh)/100;
			  			xp = [_edmm * _dpmm, _pw - w - (_edmm * _dpmm)]?pos;
            			yp = ph - (bdmm * _dpmm);
             			t = (floor Options.thick.value * _ow')/160;

          			bg = image_new (get_width nim) (get_height nim) (get_bands nim)
                 		(get_format nim) (get_coding nim) (get_type nim) 0 0 0;
            		   draw_block xp yp w t nim =
               			draw_rect_width xp yp w t true 1 [255] nim;
            			label = im_text text.labels?text Options.font.value w 1 (_dpi*(_ow'/160));
            			lw = get_width label;
            			lh = get_height label;
            			ly = yp - lh - t;
            			vx = [xp - t / 2, xp + w - t / 2];

						scale = (draw_block xp yp w t @
							draw_block vx?0 (yp - 2 * t) t (t * 5) @
							draw_block vx?1 (yp - 2 * t) t (t * 5) @
							insert_noexpand (xp + w / 2 - lw / 2) ly label)
							bg;

				}
			}
		}
	}
```
