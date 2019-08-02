# Dependencies
* [nip2](https://github.com/libvips/nip2)
* Follow the [provided instructions](https://github.com/jpadfield/nip2-extras/blob/master/README.md) to add this new tool to [nip2](https://github.com/libvips/nip2). 

# Acknowledgement
* This function was created by [jpadfield](https://github.com/jpadfield)
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
* For this example the new tool "Image to non zero colour" was added to a new Toolkit called "Extras".
* In the main (workspace) window:
  * Create or open an image to be processed.
  * Select the image by left clicking on the alphanumeric tag tot he left of your image, this will be **A1** for the first image loaded into column **A**.
  * Run the new function **Toolkits > Extras > Image to non zero colour**.
* Please note, in the example shown in the screenshot below an **Arrow** and the function **Image > Select > Rectangle** was used to create the image used to test the new function.

# Screenshots 
<img src="https://github.com/jpadfield/nip2-extras/blob/master/images/nzc_01.png" width="512" alt="Example Screenshot">
 
# Tool Code
* [non_zero_colour.def](non_zero_colour.def)
