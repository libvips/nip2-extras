# Dependencies
* [nip2](https://github.com/libvips/nip2)
* Follow the [provided instructions](https://github.com/jpadfield/nip2-extras/blob/master/README.md) to add this new tool to [nip2](https://github.com/libvips/nip2). 

# Acknowledgement
* This function was created by [jpadfield](https://github.com/jpadfield)
* The work was carried out as part of the general image processing development at [The National Gallery](https://www.nationalgallery.org.uk/)
<img src="https://github.com/jpadfield/nip2-extras/blob/master/images/NG Logo Black on Transparent 600.png" height="64" alt="IPERION-CH Logo">

# Summary
This function was written to quickly adjust the colours used in a 2 tone logo or text on a background colour. It was specifically created to allow multiple matching, simplified logos to be dropped into "partner" pages on project websites.
* **INPUT:** The function takes in a single image.
* **OUTPUT:** The function will output a new version of the image with adjustable foreground and background colours.

# Instructions
* Open Nip2 software
* Ensure that you have added this new tool, given below onto a new or existing Toolkit.
* For this example the new tool "Adjust logo colours" was added to a new Toolkit called "Extras".
* In the main (workspace) window:
  * Open the existing logo image to be processed.
  * Select the image by left clicking on the alphanumeric tag tot he left of your image, this will be **A1** for the first image loaded into column **A**.
  * Run the new function **Toolkits > Extras > Adjust logo colours**.
  * This will create a new version of the image in your column with, as default, white image or text on a black background.
  * The foreground and background colours can then be changed using the two provided colour widgets.
 
# Screenshots 
<img src="https://github.com/jpadfield/nip2-extras/blob/master/images/alc_01.png" width="512" alt="Example Screenshot">

# Tool Code
* [Adjust_logo_colours.def](Adjust_logo_colours.def)

