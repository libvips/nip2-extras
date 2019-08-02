# Dependencies
* [nip2](https://github.com/libvips/nip2)
* Follow the [provided instructions](https://github.com/jpadfield/nip2-extras/blob/master/README.md) to add this new tool to [nip2](https://github.com/libvips/nip2). 

# Acknowledgement
* This function was created by @jpadfield
* The work was carried out as part of the H2020 EU project [IPERION-CH](http://www.iperionch.eu/)
<img src="https://github.com/jpadfield/nip2-extras/blob/master/images/IPERION-CH_logo_trans.png" height="64" alt="IPERION-CH Logo">
<img src="https://github.com/jpadfield/nip2-extras/blob/master/images/iperion-ch-eu-tag_black.png" height="64" alt="IPERION-CH Grant Info">

# Summary
This function was written to help export details of points and areas of interest marked on images within nip2. The initial purpose of this process was to allow users to start annotating images and stored the annotation information in a readily re-usable form, so that it could be loaded into other pieces of software. This was intially used to save annotation details prior to presenting them in the [IIIF](https://iiif.io) image viewer [Project Mirador](https://github.com/ProjectMirador/mirador)
* **INPUT:** The function takes in a group of marks and regions.
* **OUTPUT:** The function will output a copyable block of Json code.

# Instructions
* Open Nip2 software
* Ensure that you have added this new tool, given below onto a new or existing Toolkit.
* For this example the new tool "Export relative dimensions" was added to a new Toolkit called "TEST".
## In the main (workspace) window:
* Create or open an image.
  * Go to **File > Open** and select the image file.
  * or Drag and drop the file directly into the nip2 window.
* The image should appear as item (probably **A1**) in your currently selected column, showing a thumbnail along with some of the basic image metadata.
* Double click the thumbnail to open the **A1** image window.
## In the image window:
* Look at the image and determine which area you would like to select.
* Use the **ctrl + scroll wheel**, or the keyboard shortcuts (letters **I** & **O**), or the View menu on the window to zoom in/out of the image as required.
* Then place the required number of marks or regions to define or highlight the points ands areas of interest
### Place a Mark or Region to define particular parts of the image 
* To place a Point: hold down **ctrl** and click on the image. The Mark will appear as a cross and numbered flag (label).
* To place an Area: hold down **ctrl** and drag down and right with the left mouse button.
* Another way to place Mark or Region is from the menu **File > New**.
### Tools to edit or change Mark and Region:
* Marks and Regions can be repositioned by dragging the numbered label
* Left-drag on the edges or corners to resize
* Right-click on the label to get a menu that can be used to remove or edit the shape
### Read the spatial coordinates (Left, Top, Width, Height):
* Double-click on the label to get a window with four spatial coordinates (Left, Top, Width, Height).
* You can also find the spatial coordinates closing the image view window and looking at the main window. Each row has (from left to right) a pair of up/down arrows indicating that the row contains sub-rows: click on the down arrow several times to open the row up and see the spatial coordinates of your Mark or Region.
## Exporting Relative coordinates of image annotations
In the main (workspace) window:
* Select all the required Marks and Regions by clicking ***A2*** to ***Ax***, where ***Ax*** is your last tag, while holding down the **shift** key.
  * You can also select/deselect specific points, if required, by clicking on then while holding down the **ctrl** key.
* In the main menu options select **Edit > Group**.
* This will create a new group item in your selected column, which will contain a reference to all of the points you had selected.
* Select the group item, by clicking on it, and then in the main menu select **Toolkits > TEST > Export relative dimensions**.
* This will create a new entry in your column and the details of all of the selcted annotations can be exported bu simply copying the long line of text created in the text box.
* The data is formatted in a simple JSON format which can then be re-used in other programs.
## Additional Notes
* The Json output includes fields for titles and text desctiptions or comments to be added to the details, these can be very useful when the data is reused.

# Example output
```json
{"annotations": [{
	"file": "/home/joe/.nip2-8.7.0/tmp/untitled-nip2-10469-XMUUW5Z.v",
	"x": 0.1342025,
	"y": 0.516129,
	"w": 0,
	"h": 0,
	"title": "Default Title",
	"text": "Default Text."
}, {
	"file": "/home/joe/.nip2-8.7.0/tmp/untitled-nip2-10469-XMUUW5Z.v",
	"x": 0.3358896,
	"y": 0.2292627,
	"w": 0.09202454,
	"h": 0.03917051,
	"title": "Default Title",
	"text": "Default Text."
}]
}
```

# Required Code
```
Export_annotations = class
 Menuaction (_ "Export relative dimensions") 
  (_ "Export dimensions and relative positions of a group of points or regions") {
   action x = 
    _result {
     _vislevel = 3; 
     _group_check = is_Group x;
     _pt_l = x.value, _group_check
           = x;
     _str =  concat ["{\"annotations\": [",foldl dostuff "" _pt_l, "]}"];
     _result = String "Annotation" _str;    

     dostuff _s1 _s2 = _s1p2 {
      _s1p2 = concat [_s1, process _s2], _s1 == ""
            = concat [_s1, ", ", process _s2];}
            
     process r = _str {
      _iw = r.image.width;
      _ih = r.image.height;
        
      _rt = r.top;
      _rl = r.left;
      _rw = r.width;
      _rh = r.height;
   
      x = _rl/_iw;
      y = _rt/_ih;
      w = _rw/_iw;
      h = _rh/_ih;
  
      _str = concat ["{ \"file\":", print r.image.super.filename, ", \"x\": ",
       print x, ", \"y\": ", print y, ", \"w\": ", print w, ", \"h\": ", 
       print h, ", \"title\": \"Default Title\", \"text\": \"Default Text.\" }"];}}}
```
