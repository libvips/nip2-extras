# Dependencies
* [nip2](https://github.com/libvips/nip2)
* Follow the [provided instructions](https://github.com/jpadfield/nip2-extras/blob/master/README.md) to add this new tool to [nip2](https://github.com/libvips/nip2). 

# Acknowledgement
* This function was created by [jpadfield](https://github.com/jpadfield)
* The work was carried out as part of the H2020 EU project [IPERION-CH](http://www.iperionch.eu/)
<img src="https://github.com/jpadfield/nip2-extras/blob/master/images/IPERION-CH_logo_trans.png" height="64" alt="IPERION-CH Logo">
<img src="https://github.com/jpadfield/nip2-extras/blob/master/images/iperion-ch-eu-tag_black.png" height="64" alt="IPERION-CH Grant Info">

# Summary
This function was written to simplify the process of adding consistent scale bars to sets of images in preparation for publication. The initial use was collecting a set of microscope images of know resolution and then adding a scale bar to them all at once.
* **INPUT:** The function requires and image and a number (the resolution scale in ppmm)
* The function can also be run on a group of images and a single resolution value or a matching group of individual resolution numbers.
* **OUTPUT:** The function will output an image or groups of images annotated with the required scale bar. A series of options are provided as part of the output to control the colour, position, thickness and size, etc. of the scale bar.

# Instructions
* Open Nip2 software
* Ensure that you have added this new tool, given below onto a new or existing Toolkit.
* For this example the new tool "Draw Scale Bar" was added to a new Toolkit called "Extras".
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
* In the main menu select **Toolkits > Extras > Draw Scale Bar**.
* A new scale bar widget will be added to you selected column.
* Adjust the various options as required to adjust the format of the scale bar.
  * For single images the results will be shown in the thumbnail of the widget.
  * For groups of images you will need use the **Edit > Ungroup** option to unpack the group and see all of the results.
  * Please note that groups can be saved in one go.

# Screenshots 
<img src="https://github.com/jpadfield/nip2-extras/blob/master/images/dsb_01.png" width="512" alt="Example Screenshot">
<img src="https://github.com/jpadfield/nip2-extras/blob/master/images/dsb_02.png" width="512" alt="Example Screenshot">

# Tool Code
* [Draw_Scale_bar.def](Draw_Scale_bar.def)
