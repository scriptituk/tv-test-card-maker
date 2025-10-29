<a name="chmtopic1"></a>**FML Test Card Maker v5.11**

Test Card Maker is intended as an aid to the creation of test cards and test patterns on the PC. It allows the positioning and manipulation of many basic test pattern elements, such as a grid, colourbars, greyscales and high-frequency gratings, within a rectangular image, which can then be scaled to a wide range of sizes.

Images created with Test Card Maker can be 'dumped' to a standard bitmap (.bmp) or JPEG (.jpg) file if desired; however the program uses its own format (.tcd) to store the defined patterns. This contains just the instructions needed to create the image, and is thus much more compact than a bitmap. Because Test Card Maker uses its own co-ordinate system (which you specify for each pattern), the images retain true sizeability when saved as .tcd files.

<a name="chmtopic2"></a>**Program Info & Disclaimer**

Test Card Maker - Freeware\
Version 5.11 - 27/03/2004\
Written by Steve Heap at Funsville Memetic Laboratories.

(c) Copyright Steve Heap / FML 2001,2004.

In addition to the application itself, the following files are provided:

|**CardDef.ico**|Icon for TCDs, for use in Explorer|
| :- | :- |
|**CardDef2.ico**|An alternative icon|
|**CardDef3.ico**|Another alternative|
|**barsred.tcd**|A simple colourbar test pattern|
|**tcc.tcd**|Simulation of Test Card C|
|**pm5544.tcd**|Simulation of Philips PM5544 test card|
|**clas79.fon**|A classic 7x9 'dot matrix' font for test cards|
|**clas57.fon**|A titchy version of clas79 for really chunky captions|
|**tcmhlp.chm**|this HTML Help file|

The application and associated files have been checked and found to be virus-free; however **THE ONUS IS ON THE USER TO SCAN THE APPLICATION AND ASSOCIATED FILES FOR VIRUSES**. Funsville Memetic Laboratories aka Steve Heap does not accept any liability, financial or otherwise, for consequent damage from any virus that might infect any of the files.

There is no automatic installation procedure. I have done my best to trap portability problems; thanks go to Test Card Maker users who have provided feedback.

The application has been tested in 8-bit, 16-bit and true colour display modes.



<a name="chmtopic3"></a>**What's New - Version 5.10 / 5.11**

The Viewer image can now be drawn anamorphically, i.e. at 720 x (no. of picture lines), squashed horizontally.

Extra pre-set aspect ratios available (partly to support anamorphic images): 4:3 and 16:9 with 'digital sides', 5:4, square.

"Flip/Rotate" added to Edit Menu. This allows you to reflect all the selected objects in the current layer horizontally or vertically, or rotate them by 180 degrees.

Picture objects can now be drawn transparently, with a choice of transparent colour.

New shapes available for Cutouts: diamond and four directions of triangle.

**New Options**

- Allow mouse click to close the Viewer when in full-screen mode.

**Interface**

"Select Card" added to File Menu. This has a sub-menu showing all the open TCDs when more than one is open; selecting a TCD from that list brings all its layers to the top and minimises all layers of any other open TCDs.

**Bug fixes / tweaks**

- Access violation was occurring on multiple undo followed by multiple redo when different types of edits were involved (e.g. moving an object then adding a layer then adding an object).
- The above fix **may** also have fixed a reported "Cannot load file tcl[address].bmp" error, as the palette-manager is now associated with the layer editor rather than the layer itself, but I could not replicate the bug so I can't be sure.
- Access violation sometimes occurred when opening a TCD from the File menu after closing the default blank TCD.
- Prevented "Floating point division by zero" error that occurred when trying to draw a gradient with identical start and end colours in true-colour mode. (Not an obvious thing to test!)
- "Relative pathname" checkbox now enabled immediately after selecting a New Pic (if the TCD has been saved as a file).
- "Lock aspect ratio" checkbox was not updating the actual property for Picture objects, meaning you couldn't stretch and squash bitmaps except by editing the TCD as a text file.
- "1 regions", "1 bars" etc. de-pluralised on the status bar description of the selected object.
- Viewer image height (for non-anamorphic images) is now the rounded-off result of dividing the width by the aspect ratio, rather than the rounded-down result.
- "Revert to saved version" prompt when selecting an already-open, edited TCD had stopped appearing - it has now been reinstated.
- Fixed a memory leak in the get-out when there are insufficient resources to draw an anti-aliased image (this made subsequent attempts to re-draw more likely to fail as well).

**Bug fixes / tweaks in v5.11**

- Resizing of multiple objects at once with the mouse had gone wrong in the vertical direction (was OK when resizing only one object!)
- Custom aspect ratios were not being picked up in the Editor Height property on the Card Properties panel.
- Slight amendments to Line positioning and Grating drawing in order to work better when anti-aliasing is used.

<a name="chmtopic4"></a>**Previous Versions - Notices**

These are included for anyone upgrading from more than one version ago. The full version history can be seen on the website at [www.oodletuz.fsnet.co.uk/soft/tcmhist.htm](http://www.oodletuz.fsnet.co.uk/soft/tcmhist.htm) .

**3.30**\
Fixed another 'temporary bitmaps' bug (see below) which had a different cause (clicking Cancel in the Layer Properties panel).

**2.30**\
Previous versions tended to leave temporary bitmaps in the PC's temporary directory (e.g. C:\Windows\Temp). This has now been fixed. (For C++ fans: the generic list item class needed a virtual destructor.) **Please check for these files** as they will use up a fair bit of disk space if there are a lot of them. Any files in your PC's temporary directory with names like 'tcl[hex digits].bmp' can safely be removed while the application is not running.

<a name="chmtopic5"></a>**Upgrade for Multi-File Open**

From version 5.00 onward, Test Card Maker can use DDE (Dynamic Data Exchange) to allow opening of multiple TCD files from Explorer with a single instance of Test Card Maker. If DDE is not enabled, one instance of Test Card Maker opens for each file, as per previous versions.

If you are upgrading from a version prior to 5.00, you need to amend the file type properties in Explorer to use DDE to enable this function.

**On Windows 95:**

a) Open Explorer and select View|Options from the menu.

b) Click the "File Types" tab on the Options panel.

c) Select "Test Card Definition" from the list of file types and click the "Edit..." button to bring up the "Edit File Type" panel.

d) Select "Open" from the Actions list and click the "Edit..." button.

e) Check the "Use DDE" box and enter the DDE parameters as follows:

|**Use DDE**|(checked)|
| :- | :- |
|**DDE Message**|%1|
|**Application**|Test Card Maker|
|**DDE App Not Running**|(leave blank)|
|**Topic**|System|

f) Click "OK" or "Close" on each panel to accept changes.

**On Windows XP** the the Options panel is accessed from Tools|Folder Options, and the button to edit the file type is labelled "Advanced" rather than "Edit"; otherwise the process is the same as for Windows 95.

You can still open multiple files at once from within Test Card Maker even if you do not make these changes.

<a name="chmtopic6"></a>**Known Issues**

Bullseyes and crossbars not at 45 degrees may appear uneven (this varies with the size of the image too). This is rather a difficult problem, to do with mapping floating-point coordinates onto integer pixels ... but not as difficult as anti-aliasing the stripes! Using anti-aliasing in the Viewer improves their appearance.

Because the size of text is calculated from the actual boundaries of the text, and not from the notional font height, different text can display at different sizes within the same bounding rectangle. For example "Coy" is taller than "cox", so "Coy" would be drawn using a smaller font size and/or scaled up by a smaller factor, within two text objects of the same height.

The resizing blocks for crossbars do not move with the drag areas when moving / resizing with the mouse, until you release the mouse button. The drag areas do show the correct new position of the crossbar during move / resize though.

Colour mismapping (a.k.a. colour washing) problems have now been fixed, but the Thumbnail screen often causes colour-washing on 256-colour screens because the thumbnail image is a true-colour image, whereas the main Viewer image is 256-colour. This does not affect the colours actually used in the thumbnail image.

Transparent bitmaps may draw with the wrong colours in the layer editor, and when 8-bit mode is used in the Viewer, if the bitmap is also 8-bit (or lower). This is actually a Windows problem - in order to draw the bitmap correctly, the colour white must be allocated to the last entry in the colour palette of the bitmap.

The way the viewer's full-screen mode is implemented means the switch to/from full-screen is not instant. Therefore, for a fraction of a second, other key presses/mouse clicks may be intercepted by another application on the screen, causing that application to come to the top. If this happens, Alt-Tab back to Test Card Maker, or click its taskbar button, to retrieve the display.

CD Play function may not work depending on your PC's configuration, e.g. if audio CDs are automatically played on insertion. It is possible that when you insert a CD, a program which plays the CD is invoked and gains control without appearing on screen (because Test Card Maker's full-screen viewer stays on top) - in this case you may find that another key achieves the same result, e.g. Ctrl+P for Windows Media Player, spacebar for Creative CD Player.

<a name="chmtopic7"></a>**Basic Use**

When you start up Test Card Maker, you are presented with a default TCD consisting of single, blank layer with a mid-grey background. The aspect ratio is 4:3, editor size 512x384, with a 16x12 logical coordinate grid, and no physical grid. (This automatic default can be switched off - see "Options" section.)

The menu contains six sub-menus:

- **File** - the usual New, Open, Save, Save As, Close, and Exit, plus Close All, Select Card, Properties and Viewer.
- **Edit** - Undo, Redo, Cut, Copy, Paste, Delete, Select All and Shift Set.
- **Layer** - access to layer and grid properties, and manipulation of layers themselves (see "Multi-Layer Test Cards").
- **Tools** - Colour Cruncher tool, ToneBox tool, and Options.
- **Window** - Next and Previous Window options plus a list of currently-open windows (each layer editor is a separate window).
- **Help** - Help Topics (to access this documentation) and About (gives a version information box).

**Starting a new TCD**

Click the New button, or select File|New from the menu, or press Ctrl+N to create a new TCD. The new TCD uses the same default values as the one which is optionally created on startup.

**Opening a TCD from a file**

To open a previously saved TCD, click the Open button, or select File|Open from the menu, or press Ctrl+O.

The File menu will also show the filenames of the most-recently opened or saved TCDs (including from previous sessions). Choosing one of these options re-opens that TCD.

**Saving a TCD to a file**

To save changes to a file you have previously opened, click the Save button, or select File|Save from the menu or press Ctrl+S. To save a TCD with a new filename, select File|Save As or press Ctrl+Shift+S. All these options save the required information to a .tcd file - note that this does \*not\* create a bitmap. If you omit the '.tcd' extension it is added automatically. For new TCDs (indicated by "<Untitled>" in the title bar) File|Save behaves like File|Save As.

**Selecting a TCD when more than one is open**

If you have more than one TCD open at once, the File|Select Card menu item becomes active, and has a sub-menu which lists all the TCDs that are currently open. Selecting a TCD from that list brings all its layers to the top, and minimises all layers of any other open TCDs. If the layer editors are maximised (i.e. only one is visible at a time), it just brings the layers for the selected TCD to the top. This is because minimised windows cannot be mixed with maximised ones.

Minimised layer editors appear as small rectangles at the bottom of the application workspace. Using the Select Card function does not prevent you from restoring a layer editor after it has been minimised.

**The Toolbar**

The first set of buttons on the toolbar provides another way of performing file operations - New, Open, Close and Save.

The second set of buttons provides access to [Card Properties](#chmtopic8), [Layer Properties](#chmtopic9), and the [Viewer](#chmtopic10).

The third set of buttons controls selection of areas and objects. The first button allows the definition of a selection area on the current layer, by clicking and dragging with the mouse. If you then click an 'add object' button (see below) the new object's position and size default to that of the selection area. Alternatively if you click the second button, or use the Edit|Select All menu option or press Ctrl+A, only objects lying within the selection area are selected, rather than all the objects in the layer. The Select Area button stays down until one of these actions is taken or you click it again.

The remaining buttons allow objects to be added to the current layer. Each button has an icon showing the object type that will be added. The status bar and tool-tip also indicate the object types when you move the mouse over the buttons. Clicking any of these buttons brings up a 'properties' panel appropriate to the object type. Click the 'OK' button on this panel to add the new object using these properties, or 'Cancel' to stop creating the new object.

Once an object has been added, its properties can still be altered, either by double-clicking on the object's [active area](#chmtopic11) , or by editing it from the Layer Properties panel's object list. In either case this brings back the Object Properties panel. This panel also has a 'Delete' button allowing the removal of objects. Note that if more than object is selected, only the object you double-clicked is deleted, not the whole set.

<a name="chmtopic12"></a>**Test Card Definitions**

A single Test Card Definition ("TCD") consists of one or more layers. Each layer may contain elements ("objects") such as colourbars, greyscales and text; the second and subsequent layers can each be added transparently (i.e. background does not obscure lower layers) or opaquely with a specified background colour. 'Cutout' regions can also be defined, through which lower layers are visible. (Obviously an opaque layer should contain cutouts, but a transparent layer can also have them, affecting the grid and objects on that layer.) These layers are then combined to create the full image.

All layers share a logical coordinate grid, against which the position and size of each object is measured. Each layer can also have its own physical grid.

The types of object which can be incorporated are as follows:

- Colourbars
- Greyscales
- Solid or alternating-colour blocks (e.g. castellations, low-frequency gratings)
- Colour gradients
- Single straight lines
- Circles / ellipses
- Boxes / frames
- Crossbars (corner stripes as seen on Test Cards C, D, E, F)
- Triangles
- Crosses (horizontal and vertical lines with optional solid background)
- Gridcrosses (extra styling on gridlines as seen on Test Card F)
- High frequency sine gratings
- Bullseyes (sets of concentric rings as seen on many optical test cards)
- Frequency Bursts (an more versatile type of grating)
- Sweeps (gratings of smoothly increasing frequency)
- StarBursts (radial frequency grating)
- Lightspots (three optionally overlapping spots with colourbar colours)
- Text
- Clocks (time, date or countdown)
- Pictures
- Cutouts

For each of these, a position and size are specified, plus several other properties e.g. colourbar intensity, grating frequency, line thickness. Position and size are relative to the logical coordinate grid. There can be any number of each type of object in each layer of a TCD.

Each TCD has several properties which can be amended, and which apply to every layer defined within the TCD:

- Title
- Aspect ratio
- Layer editor size
- Coordinate grid size
- Border size
- Forcing of square grid cells
- Alignment of grid to pixels (i.e. forcing each cell to be exactly the same size)
- Effective TV line frequency (for defining frequency burtsts in MHz)

The following properties can also be amended separately for each individual layer:

- Transparent or opaque background
- Background colour (if not transparent)
- Grid thickness and colour
- Position of physical grid relative to the card's logical grid

<a name="chmtopic11"></a>**Using the Mouse with Objects**

You can also move and resize existing objects with the mouse. Objects are moved and sized in steps of 1/4 of a logical grid cell, unless both left and right mouse buttons are held down, in which case movement is to the nearest pixel.\
Clicking on the 'active area' of any object draws a dashed line around this area, and blocks for resizing at the corners and edges. The object can then be dragged and resized in the standard way. The mouse pointer changes to indicate the kind of move or resize that will occur.

For most objects the active area is the rectangular or elliptical footprint of the object, but there are exceptions:

- Line: click on the line itself.
- Cross (if transparent): and GridCross: click on or near the cross itself.
- Frame (transparent box): click on or near the edge of the box.
- Circle (if transparent): click on or near the edge of the circle.
- Corner stripes: click on one of the four corner cells.
- Cutout (if not rectangular): click on the area of the cutout shape itself.

Multiple objects can be selected as follows:

- Hold down Shift while clicking an object to add it to the selected set.
- Hold down Ctrl while clicking to switch the clicked object into/out of the selected set.
- Click the Select Area button, drag the mouse to define the selection area, then use Select All to select all objects in that area (and de-select other objects).

When more than one object is selected, the resizing blocks encompass the whole set, rather than there being individual dragging blocks for each object. When resizing more than one object at once, each object in the set is resized proportionally within the rectangle which bounds the whole set.

Double-clicking a selected object still brings up the object properties panel for that object alone, and does not un-select other objects from the selected set.

**Limitations to Moving and Resizing**

If you resize an object (apart from lines) to have zero width or height with the mouse, it is instead given a width or height of 1/4 of a cell. This is beacuse zero size is not allowed for these objects. (The minimum size actually allowed is 0.01 of a cell, but this might render the objects invisible in the layer editor.)

Corner stripes have special behaviour when dragging, as their corners must always be symmetrical about the centre of the card. If you drag one of the corner stripes' corner cells when other objects are also selected, the other objects will moved in concert with that corner cell, but the other corner cells will move differently to keep the stripes symmetrical. Dragging one of the other objects instead causes the corner stripes to be repositioned as if dragged by the left-hand corner. This is just something that the program had to either handle somehow or disallow altogether!

If you resize a picture object that has fixed aspect ratio with the mouse, its shape will not change, meaning that it may not occupy the whole of the dragging area when you finish re-sizing. The dashed outline of the object shows what its position and size will be.

You cannot double-click, drag or resize objects while the Select Area button is pressed in. As with move/resize operatons, the selection area changes in 1/4-cell units while dragging, unless you hold down both mouse buttons.

<a name="chmtopic13"></a>**The Edit Menu**

This provides the usual Undo, Redo, Cut, Copy, Paste, Delete and Select All options, plus Shift Set and Flip/Rotate (see below).

**Undo, Redo**\
The 5 most recent edits in each open TCD can be undone and redone, and this works for any kind of operation - on card properties, layers, single objects or sets of objects.

**Cut**, **Copy, Delete**\
These act on the currently selected objects within the currently selected layer.

**Paste**\
Pasted objects become selected objects, de-selecting the previous ones but not removing them - even if they have just been Pasted themselves. If you have more than one TCD open, you can cut or copy objects from one TCD and paste them on another - note that the Position and Size properties of the objects are preserved, rather than their physical position and size on the card.

Pasted objects are always placed on top of the existing objects in the layer (apart from cutouts, which always have to be on top), but the order of overlapping within the selected objects is preserved in cut/copy/paste operations, regardless of the order in which the objects were selected prior to cutting/copying.

**Why Paste can seem not to do anything**\
If you Copy and then immediately Paste objects in the same layer, the new objects are identical to the copied ones, and they also become the selected set. Therefore, nothing seems to have happened - but moving the new objects reveals the original ones underneath. This has the advantage that if you create objects in the right position but the wrong layer, you can simply Cut them, go to the correct layer, and then Paste them there instead.

**Select All**\
This selects all the objects in the current layer, unless the layer has a selection area displayed, in which case only objects within that area are selected and any others are de-selected. Only objects that are entirely within the selection area are selected, but the Edging property of objects is ignored in this case.

**Shift Set...**\
Select this option to fine-tune the position of the currently-selected set of objects. Choosing this option pops up a panel for you to enter the horizontal and vertical shift amounts. This can be useful when you need to repeat a set of objects symmetrically in each corner, if dragging with the mouse does not quite give the correct position for the repeated sets.

**Flip/Rotate >**\
Select this option to reflect all the currently-selected objects horizontally (Mirror) or vertically (Flip) or rotate them by 180 degrees. The operation is performed within the rectangle that bounds the set of objects, so the set taken as a whole stays in the same place, rather than the individual objects each staying where they are. 

<a name="chmtopic14"></a>**Custom Controls**

Several properties are maintained via edit boxes with associated up/down buttons. These are customised controls with the following extra features:

- Holding down Ctrl may allow fine tuning. For example the Size and Position values change by 0.25 with a normal button click, but by 0.01 when Ctrl is held down while clicking.
- Where fine tuning is provided, holding down Shift while clicking the buttons changes the value to the next multiple of the normal increment (a kind of 'snap to grid'). For example, clicking the '+' button on a Size or Position value of 3.33 changes it to 3.58 normally, but to 3.50 when Shift is held down.
- Clicking on the buttons moves the focus to the edit box.
- The up and down arrow keys activate the up and down buttons of the control when it has focus. Shift and Ctrl can also be used with the arrow keys.

Thickness-type properties use one of the above customised controls plus two radio buttons, 'Pixels' and 'Cell %'. These allow you to specify the thickness as an absolute number of pixels or as a fixed percentage of the width of a grid cell.

Colour properties are shown as squares or rectangles of the chosen colour. Click the shape (once only) to bring up a colour selection panel. This panel is itself customised (see below).

Note that the colours shown in these controls may be dithered colours if your screen only allows 256 colours. This does not affect the appearance of the card, in which the colour palette is adjusted to include all the colours your objects need. The colour selection panel is itself a custom control (see below).

Some properties are maintained by custom graphical controls (such as the edging and text alignment controls). The operation of these is described in the relevant detailed section.

**The Customised Colour Panel**

This provides different preset colours that are more useful in test cards, and allows you to set a colour using the PAL Y/U/V components (in addition to the traditional R/G/B and H/S/L controls).

Initially the dialog is shown in compact mode - click the "More>>" button to see the full display with colour wheel, brightness slider and value controls. When in compact mode, the R/G/B values of the currently selected colour are shown on coloured labels.

The range of the H/S/L controls is different from a standard colour panel:

- Hue runs from 0 to 359 (0=red, 60=yellow, etc)
- Sat runs from 0 (grey) to 256 (full sat)
- Lum runs from -256 (black) to 256 (white).

The Y/U/V controls are as follows:

- Y = brightness, range -256 to 256 (as per Lum above).
- U,V = 'blue' and 'red' colour differences - these actually give the purple (+U), yellow (-U), pink (+V) and green (-V) colours seen on the PM5544 when one is varied while the other is kept at zero.

The allowed range of each value depends on the other two values, but is always within -256..256.

The standard PAL transformation is used for YUV values:

![](data:image/gif;base64,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)

where r=0.299, g=0.587, b=0.114.

A 0..256 range is used internally for translation between R/G/B, H/S/L and Y/U/V: as only 0..255 is allowed in 24-bit colour, the R/G/B values shown are 1 lower for values greater than 128.

The 'Store' button adds the current colour to the list of custom colours, if it does not match any of the existing custom or basic colours. Up to 22 custom colours can be stored, and they are remembered when you close the application. If you press 'Store' when all the custom colours are used up, you can then click one of the custom colours, which will replace it with the new colour.

You can also right-click on any custom colour to get a pop-up menu with options to clear that colour or clear all custom colours (the latter has a confirmation box).

<a name="chmtopic15"></a>**Multi-Layer Test Cards**

Simple patterns, and even complex ones such as Test Cards C and D, can often be created using a single layer. However, when objects are required to be clipped to a circular area, or small parts of a grid need to be shown, a different technique is required. This is the technique of multiple layers and cutouts.

Each layer in a multi-layer test card is numbered; the layer editor also shows you the total number of layers (e.g. Layer 1 of 3, Layer 2 of 3, Layer 3 of 3). When you draw a multi-layer test card in the Viewer, Layer 1 is drawn first, then Layer 2, and so on, so higher-numbered layers are drawn on top of lower-numbered layers. When editing a multi-layer test card, each layer gets its own layer editor, and cutouts are shown as cross-hatched areas. If you have more than once TCD open at once, the layer editors also indicate to which TCD each layer belongs.

**Multi-Layer Test Card Example**

![](data:image/gif;base64,R0lGODlhNwFaANMIAAAAAIAAAACAAICAAAAAgIAAgACAgMDAwICAgP8AAAD/AP//AAAA//8A/wD//////ywAAAAANwFaAAAE/hDISau9OOuNn/dcKI4k9YFlqqrns74wh8x0PS94jjt8zyvAILBBLBITyCSSwWwybVAEoAWoPaJXaNa2tWK/WrCUGi2bz+i0ejY9VWlduNgbrnPncvb7rNP5fEJCRkZKSk5OaW0fewhxM46NeI+SkXZ0Y25rmpucZ4ogl6F5d5ajopN2Eml9OX89gUGDRYVJh02JZKa6qKS9p5W+o58uncXGmsOMkMuUzKW8l6porDuuDrBDsg20S7YMuG4t4uPk5ebn6OGZx+ztNsnp8fLz8dJ81NbX2Nrb3N7faJL9ctYrwy5gA2kIdMeQ3UJoBwkKMhKxmUJGZagtyIdNAT9u/gn+gVuU8JkUClJSVqlgMVWuhjA5PURYEUrHjy0LYoyikeM+bSBFBnxJEyJECVn2TGGj0AVGgtGIxpw6dJ3RojR//JSVJNjVLfbM9LR2E6g/byNB1dS5UqXbtnDtQRUmlapdKDPn8gK0dVChtdF2QhnrqizXs7bSEgOcp20jpY8gP1b4VczMu5ibWsXq7I9hv385WxZsg7DnvoQQH1KsrJkquG9jw1651CTYupnv5m1GFvUsbnqBhc2Irzesj6oRVSXJmGlKNkmbOh8zfXhl6JtzY95t0udxs7QAehVOuoZpvt8Ph0e7HAQ9FC7iT5kvvz79+/KHpbus3S689xsZ/hcIcuu9Z91gxRXm2xHJ3dLeYtdRBuEbE0ZG2WTOOTXebdn1RxV3wVSjYHqgrSdehAeWluBpJKZm4moPtlbKbLLVSCNsJWHCnIe6ETWXiCwOCF4hDq6VonkroiekekSy54mPc6wUHXTVTUndc1fKWBBuPDYEYiitCDgRk4YUKZoeqyT5yoL9vKjck5sRdKONdM65h5xcdunOl6P4IWYsQ5ZZpJzl0XDemi3+5qaZZfDJizQVYvhcpJS+cadleerpEJR2+DnikiU2OehoabLiHaguigojnDue+VqdsNp5EoqZamqMo5X0ceqYoQrqIKGl6vpnNmTW4qQZuFpZm1LK/jZbJVMUYtqhre0ke4OnQfKaqq9PnDnrNGpqlSiDi3bLqnv72acufuyu665+4/BH7abqoGPqsB4Fauwh+xV67b2faquoqm8iy+kdllqYoWSVXjhhFXhOO++tB3sBcLaAFtvNasCCe7GSApNLMKNRWCvrybHGFvEiBLTs8ssIvNwyDTK7XEPNOOes887J7ByzzDnkLMTORBeN85GGhqvPuG2ObK7BcX5hz7LSYUk1lVZPCbG0LJPj8gkE/EzABy0/EDbNXo89jtpkg+11z2mzbfYCX3tQNgFDp+11C3LLDTbS/wobcMa97rsq1K0u8yrKjNdZ25ZulG123ZSHrXbd/mbfPLndY1d+9+WVb745AT2DLnnldHPONt5BdA765Ka7rvrrp3cOOAKHiovqwNySjFfFcDAsvMPDL0zZ41FlcvnPdsfc/OliZ06z55bP/jLnsF+fvUDLQ3853Zc78DXrQGj/cgOxm++6zLPfnvvSu4vc+9ONAh9Z4/g7vjIopnPufOagm97ZbLA8tI1uenaTngEHyD3V+e97oOuBy7BxOSPQbgmnM1sXCvite3wMUfFr2vxOVL+oacExWaoas56VNRZCjiR+m9wMutc8NXDwf2TTnP90yEAyxHBm/yNA6sw2rAoWwW8E6MbqxsbDiwQLWyAj3LYMV7ASLqJf78pi/ru2aB94UcGHDpQhDaVXMyjckHY3C2ATsXPF/o3ObkMkAA9qBgsjEuGCIWFA7fiWQBQ8MUyDI1bhNnY4K6rlK8WbVCIptMgrvZB/zxtj9cQINjPWcIaz09wNg6gZGEbyeXCMYN/qaDcLzk6JGtTgGjsoFqV9ZoqErGLJ7PeY/NlSNsiji/JqKEnmAVCNq+Sk2Ma3Q0wqsIFkBOXcTic+0JHSbKY0GxJqlkogGpOB/sKdK9kUlGMZEkKcQeHVUoi1FbbwnI90Qe3W+cDZXRKBMvTl9dgJO3merXTuhB3n4ki5OoLujrETnefsiSaPCQ5jgoRlHhMTo4EsLmW3jMv+/tQZt0pirpgG5OXe2mbRSuoIBDEMYyglRzbytQ5sd9xoH3PYt4J68KBRTCjvqOi7d9DyCgmTFCOJx1PjoWmiAPBZGWc4VALKjKhGK+NQS5ezYbYsaDWDX/lkBtCkHnWp2XzfK2cay5rWwGQQDausgDoxL91Um1AEYchESNNvdOyladXdWrvJ0HOBkxlTc9Y5zclXppC1rHs66wflKkWuLhQRb23lYKVaWPm1lYSzrNc5uEhZLVoWHfICrEy+mI7FbtWxXWVAv/4IpJjmS2OHleXvTEgKxzTMp4rs6aS4dkjNUoy1dICpWhvL1q6iKKvbZBpdCxnZxIHhoRGNVbRc/iIx267BWmgt7W5lCtrUAiSxxPEsNxtEv+LWVk7lVKF4w1vOSzG3Vc7dLG77BEiEnnaQqTUScLUrXO5CdrXGTYVY94vCv6a3E9CN7q54O1zxYJcnwQ1hgb3aye9GSWGxhe1Ojael5KH3v889a9ICFMj3KrRgB0YQfRVsX9bkCFr8TVmOMothu1ZYF9IlLHV7u9ANOdGgcWXsjBfcXfw6eEbjDLJeV/gU2oKzxWoI8LUGvGPE2NilitWtjD1sWKG4+D1OsWxl2eVFc7AYyd6ND4CYTOXqMsFA85WyjstMYysj7sfjmRqEJxzh5wjGv2A2cXMQQGYCESkn7kvwXEvc/tA9ayi5EgV0rfLc4LvypsN+VkJwwJLmHH+2zd4M84uv01fypnC5T/7okRn9zU2fyb2RTkCEAkNaDqNaX6G9r03X+9uIykXRzSV1o01NENNG2tA3hmt7fQ1r6/Z41vkNtR5eq8gi22bXui70qnUxZQIpWxiVHvZ02cxjWX9Vw3FGyWxQ8uzz1jbaPnZ0uW1waVWvm9U41na1i+3mUp9YvhcAtrlHjW5o67sX2vo3vIUd4zWnOtaswbLCF47ZRZP6PwyPuMQ1FO+Ct5vQLr73tDfuLQufu9/+5vikc7LibFt8u+Xydsg7LvCWP8rhjFayy1le6xjY/OZUuLnOYZDz/p37vAQ9/7nQOTDxohv96EhPutKXzvSmO/3pUI+61KdO9apb/epYz7rWt871rnv962APu9jHTvaym/3sTkeK1dWOdLZL3QRLdzvUK8D0Dhxd7kXH+9z1LnG+153uSvd74C0Qd7vnXRFdRnPV4d72xCed7YJneOQbvwjHL1zuk5+H2jNfDy/CHfKIdztSMD8fy2OZ758PfeU/MXrWq37w5Eh95VfvhtKXg/OKr33tkzGB2cMny4CPuN4JD3oU9N74mP895cVB/NcHP/jMN/3p4dV83z+f8bv/e85XD3rZ/771xxe+4zdv+yx/X/C41/z429B65ZM/8emnR+TJb/7i/july+F//AV8X3/92J/+h3d7x9d+9+d9Agh7sTeA5bd/5peATed3svd+BniAgwd9DHh91sd+0odF8bKAHgh487eB6ueA9CeBCkiB2teB/dd/IEh9r6d/tId84deCGah8feeC57eC0TdZIigPw6eB8AGA26eCaYeDKyiEuhd9QIiAxmeDRPh+OXh4Lch4+Ud4DeiA+jeFMyh6NKiE2Hd3VmiF97d7J9iB+bd8/BeGWliGX6hwDDiGUEiG/IeFjXd9Hxh0c8h9Z2h0b9h7cch9eZh9KRiDBSiHtCeEe7h3PWh2iYh2XhZ/jhiJOyiJmLWIaAeJlEiJjZiJTciJj2iJ/p4YiqI4iqRYiqZ4iqiYiqoYL2L2gJrXij4Ii2JHH6tYi7GHLq4Yi7I4Wbg4duxni8CoDuXXicSYhK1YehqIeFfkh6/IjMm4jK6njFwojcR4h6AYjJHofLj4i70oZtzojdsYjsdYD1dUf+W4eeKIjuNojuiijsqIjbX4jrv4jczHWeC4ju8oj7zYjqyIj/XYjffoj/wIkPBoivIYet33j+V4j/l4jgu5jwFZiOs4huIokQipjgF5jQVZdgdZkQ8piw0pkBlJjgMpkv6Xjg4JkCG5ixtJih3pjd/4HzFZkjM5kRBZkxiJk9y4hC+5khrZkr5YkaNHiMZokc8IiMD3NIpJOXs1SZH5oXv0OIPnSItAiYo/+XQieJUKGXhVqYpaGXcG0nZ115VkWZZmeZZomZZaFwEAOw==)

**NB** For Layer 1, the 'Transparent Background' setting is ignored, and any cutouts are also ignored, but they are not lost. This is so you don't lose transparency or cutouts if you move a layer to become Layer 1 and then decide it shouldn't be Layer 1.

**Using cutouts**

Where a layer has an opaque background, it will completely obscure any lower layers unless it conatins cutout objects. These effectively cut a hole in the layer, allowing the lower layers to show through the hole.

The most common use of cutouts is to give a circular border to a region containing several objects - as seen on the Philips PM5544 for example. The colourbars, greyscale etc are placed on a lower layer, and the layer above it is opaque with a circular cutout in the middle, allowing the objects to show only within the cutout region.

Cutouts are always placed on top of any other objects in the same layer. If they overlap other types of object, those objects are also cut away according to the shape and position of the cutout. For example, you could use this to create an object with a concave edge or with a hole in it.

**Using transparent layers**

A layer with a transaparent background does not obscure any of the image that has been built up from lower layers. The background is not filled in for such a layer; the objects are drawn straight on the image as if they were part of the next lower layer. Therefore, transparent layers are only really needed in some special circumstances:

- Making an object overlap a cutout (e.g. a wide text caption which will not otherwise fit anywhere into the card).
- Drawing a grid on top of some objects (e.g. a Canadian variant of the PM5544 has altered PAL bars at the sides, which have gridlines drawn over them).

Where a layer has both a transparent background and cutouts, the cutouts remove the relevant portions of the grid and any objects that they overlap.

**Adding a layer**

Select Layer|Add or Layer|Insert from the menu. 'Add' puts the new layer at the top of the card, and 'Insert' puts it just below the current layer, renumbering the current layer and any higher ones to accommodate the new layer. For example if you have two layers already and Layer 1 is selected, Layer|Add creates a new layer as Layer 3, whereas Layer|Insert creates a new layer as Layer 1, moving the existing layers to become 2 and 3.

**Removing a layer**

To remove the currently selected layer and all its objects, select Layer|Remove from the menu. This has an "are you sure" prompt. There must always be at least 1 layer in a test card.

To remove the currently selected layer and put its objects on to the layer below, select Layer|Merge from the menu. This also has an "are you sure" prompt. You can do this with any layer except Layer 1 (because there are no layers below Layer 1).

**Changing the order of layers**

Use the Layer|Promote and Layer|Demote menu options to do this. These increase and decrease the current layer's number respectively, i.e. Promote moves the layer nearer to the top of the card, and Demote moves it nearer to the bottom.



<a name="chmtopic8"></a>**Card Properties**

This section details the card-wide properties, affecting all layers of the currently-selected TCD, which can be modified via the Card Properties panel. This panel is accessed from the File|Properties menu option, or from the graphic button showing a whole test card.

**Title**\
Use this to enter a descriptive title for the card (e.g. "Modified Test Card 'D'"). This is then displayed in addition to the file name in the title bar of the application. Up to 200 characters are allowed.

**Aspect Ratio**\
Determines the ratio of the card's width to its height. There are several pre-set ratios available: 4:3, 14:9, 16:9, 5:4 and square. Alternatively 'Custom' ratios can be defined. With 4:3 and 16:9 you can also add 'digital sides', which expand aspect ratio by a factor of 40/39, corresponding to the slightly wider picture area available on digital television.

**Layer Editor Size**\
Sets the size in pixels of the panels used to view the layer(s) within the card. If the Aspect Ratio is set to 'Custom', width and height can be adjusted independently and this determines the actual aspect ratio. Otherwise, the ratio is fixed, so changing the width changes the height automatically. Note that this is not a true property of the card, except insofar as it affects custom aspect ratios. Only the aspect ratio is saved in the TCD file.

**No of Cells**\
Determines the size of the logical coordinate grid. The grid is always centred in the layers, e.g. if a 16x12 grid is specified, the points (0,0), (16,0), (0,12) and (16,12) will be symmetrically placed around the centre. This means that (0,0) is not necessarily the exact top-left corner of the layers (useful for adding border elements); however (0,0) will always be somewhere in the north-west quarter of the layers.

**Min Border %**\
Allows a border to be left around the basic grid, as a percentage of cell height/width; this is one way of forcing (0,0) away from the top-left corner. If neither 'Square cells' nor 'Align to pixels' properties are checked, the figures are used as exact border widths, otherwise they are minimum widths.

**Square cells**\
When enabled, forces the grid cells to be square (however well or poorly the 'No of Cells' matches the card's aspect ratio). Unchecking this property allows rectangular cells, whose shape is then determined by the numbers of cells and the border sizes.

**Align to pixels**\
When checked, the calculated cell size is rounded down to a whole number of pixels, ensuring that the grid cells are all exactly the same size as each other, at whatever size the card is drawn. If this property is unchecked, the exact cell size is used internally, only rounding off to the nearest pixel when drawing; thus, some rows and columns of cells will be one pixel taller or wider, but this ensures that the same amount of border is always visible, relative to the cell size.

**Line Frequency**\
This property affects frequency bursts that are specified in MHz. The available options relate to various TV standards that are or were in use around the world, and are specified as [number of lines in picture] x [frame frequency] (e.g. 625 x 25). Apart from this it has no effect on the way the card is drawn in the Viewer. 

<a name="chmtopic9"></a>**Layer Properties**

Individual layers have a few properties that can be amended in the Layer Properties panel. This panel is accessed via the Layer|Properties menu option or the graphical button showing one layer above another. 

**Background**\
If Transparent is selected, and the layer is not layer 1, then no background colour is used, and only the layer's grid and objects are drawn in the final card, otherise the selected Colour is used to fill in its background. Transparent layers still allow the background colour to be chosen so that you don't have to reset it while experimenting, and because the background is always filled with colour in the Layer Editor.

**Colour**\
Click on the coloured rectangle to set the background colour of the layer. If the layer has no cutouts and is not layer 1, the layer is transparent so this has no effect on the completed test card. 

**Show Grid**\
Check this box to access all the grid properties; when it is unchecked, the layer's grid is not shown and only its thickness can be altered. (An invisible grid may be required in a transparent layer, for correct alignment of objects in that layer with those in a lower layer that has a thick grid.)

**Thickness**\
The thickness of the physical grid lines, specifiable either in pixels or percentage of cell width.

**Colour**\
The colour of the grid lines. Click the coloured square to select a colour.

**Centering**\
Determines the positioning of the physical grid lines relative to the logical grid. For both horizontal and vertical lines, the physical and horizontal lines can either coincide or be interlaced (i.e. at half-cell displacement to each other). The control shows a cross of gridlines and a circle that can be moved to four different positions - at the cross, on one or other line, or on neither line. The position of the circle shows the position of the intersections of one grid relative to the other. For example if you place the circle on the horizontal line only, the vertical logical and physical gridlines are interlaced but the horizontal ones are not. Clicking on the diagram moves the circle and changes the property.

**Clipping**\
When checked, prevents drawing of the gridlines beyond the edges of the logical grid (can be specified separately for horizontal and vertical lines).

**Objects**\
Lists all objects defined in the layer. When a layer is drawn, the objects are drawn in bottom-to-top order of this list. Basic properties for each object are shown as follows:

**Type**\
The type of object, e.g. Greyscale.

**S**\
An S appears in this column for objects that are currently selected.

**Position**\
The defining position of the object 

**Size**\
The defining size of the object

**Count**\
The defining number of regions in the object - usually the number of different-coloured areas, but can be the number of colours used (for smooth gradients), period in pixels (for gratings) number of bars (for corner stripes, frequency bursts and starbursts) or frequency in 10KHz units (for frequency bursts in MHz). This is left blank for object types which have no such meaningful number, such as text and cutouts.

The two 'arrow' buttons allow promotion/demotion of the currently highlighted object in the list (in case objects overlap each other in the wrong order); you can also drag and drop objects within the list using the mouse. Note that cutouts always appear at the top of the list - you cannot move another object type above a cutout.

The 'pencil+tablet' button to the left pops up the Object Properties panel for the current object, and the 'tablet+X' button to the right deletes the current object. There is no confirmation box for deleting an object, although if you Cancel, deletions are ignored along with all the other changes you made while the Layer Properties panel was open. 



<a name="chmtopic16"></a>**Object Properties**

This section gives details of the properties of the various object types which can be maintained via the Object Properties panel.

There are a lot of properties, many of which do not apply to all object types. The following properties apply to all or many object types:

**Position**

X and Y coordinates of the upper-left corner of the object, shown as "X , Y".\
The coordinate system has (0,0) at the \*upper\* left corner. This is the standard way that graphics packages arrange their coordinates - the use of "+/-" instead of arrows on the up/down buttons makes this look less counter-intuitive.

**Size**

Width and height of the object, shown as "Width x Height". More precisely it is the size of a bounding rectangle in which the object is drawn.

If a Position and Size combimation means that the object may be completely off the screen, the X/Width or Y/Height values turn red, as a visual warning.

**Edging**

This is the way the edges of the object align to the physical and logical grid lines. The Edging control is a square divided into left, top, right and bottom quarters. Each quarter is subdivided into four strips, allowing each edge of the object rectangle to lie at the outside or inside edge of the physical or logical grid. (The logical grid's lines are always 1 pixel thick.) 

![](data:image/gif;base64,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)

This diagram shows where the top left corner of an object (the blue rectangle) will be drawn for various top and left Edgings, if its Position is aligned to the grid. The physical grid is 5 pixels thick; the 1-pixel logical grid is shown slightly darker, and the images blown up by 2x, for illustrative purposes. The right and bottom edges are treated in a similar way by the rest of the Edgings.

More generally, the edges of the object's rectangle are adjusted by amounts relating to the grid thicknesses, even if the Position and/or Size values are not whole numbers, or if the physical and logical grids are not aligned. Try experimenting with this control on a thick grid to get the full flavour of it.

Line objects treat Edging slightly differently - the logical grid is treated as 0 pixels thick, i.e. there is no difference between the second and third band of Edging. (This tweak was necessary to ensure lines are drawn in the right position when anti-aliasing is used in the Viewer.)

**Direction**

The direction in which the object's sub-regions run. This is another custom control, consisting of four arrows pointing up, down, left and right. The highlighted arrow shows the current direction; click on another arrow to change it.

**Thickness**

Specifies the thickness of line used to draw objects that use lines (not including gratings / freq bursts).

**Regions**

The number of sub-regions (e.g. distinct coloured blocks) within the object.

**Colours**

The colour or colours used by the object. All objects require 1 or 2 colours to be specified. Where more colours are used, they are generated from the specified colours in a manner appropriate to the object type. Either one or two coloured shapes are shown on the panel, indicating which colours will be used. Where two colours are shown, a 'swap' button becomes available (for most object types) to allow quick switching of the two colours.\
Note that 'Colours' is highlighted - click on the label to view a list of the colours which the object will actually use, as RGB values. Clicking on a row in the list causes that colour to be displayed in the square below the list. If you click the 'Store' button next to the coloured square, the selected colour is added to the custom colours on the colour selection panel - if this is full, the colour panel will pop up, allowing you to choose a custom colour to replace with the new one. This is particularly useful for objects where you do not specify all the colours explicitly, such as colourbars, and you want to know and perhaps re-use the actual colours of the object.

**Transparent**

If this is checked, part of the object is not drawn, giving a transparent effect. Therefore, Colour 2 is usually unavailable for transparent objects.

The affected parts of objects are:

- Block-train: alternate blocks
- Circle/Ellipse: the inside of the circle/ellipse
- Triangle, Cross, and Text: the rectangular area defined by Position, Size and Edging.
- Bitmap: any pixels of the specified transparent colour.

If unchecked, the affected part of the object is filled in with Colour 2.

**Other Properties**

The sub-pages in this section give a description of other properties, and any variations on the common properties listed above, for those object types that have them.

<a name="chmtopic17"></a>**Colourbars**

The following special properties and are available for Colourbars

**Colours**

Two colours are displayed. Colour 1 can only be white or yellow, and colour 2 can only be blue or black (hence the 'swap' button is not available). The sequence of colours in colourbars is always white, yellow, cyan, green, magenta, red, blue, black; the two colour settings determine where to start and stop in that sequence. This also fixes the number of regions, so the Regions property cannot be directly altered. Note that pure (saturated) colours are always displayed here, whatever shades of colour are used to draw the object.

**Colour Adjustment**

Allows adjustment of the actual shades of colour used.

**L** varies the luminance of the colours (a positive value pushes the colours toward white; a negative value, toward black).

**S** varies the colour saturation (100 = maximum colour; 0 = no colour).

**C** only has an effect when "S = chrom" is checked; it varies the luminance contrast (100 = maximum; 0 = none). For example when C=0 and L=0, the colours all set to 50% grey, whatever the S value.

**Pure B+W** when checked causes the other settings to have no effect on the black and white blocks (if included). When unchecked, black and white may be modified to shades of grey. This option has no effect on the coloured blocks.

**S = chrom** means that the S control works like the colour control on a TV: the luminance of each individual block is retained when S is changed, so for S=0 a greyscale appears. If this is unchecked, all colours move toward the same shade of grey as S is reduced, that shade being determined by the L value.

<a name="chmtopic18"></a>**Greyscale**

The following special properties are availble for Greyscales.

**Colours**

Colour 1 can only be black or dark grey, and colour 2 can only be white or light grey (hence 'swap' is not available here). Dark grey colour 1 means "exclude black" and light grey colour 2 means "exclude white". The number of regions can still be independently amended; the shades of grey produced are always on a linear scale, but account for the exclusion of black and/or white. Hence a four-region greyscale would have the following intensities depending on whether black and white are included:

|Black|White|Intensities|
| :-: | :-: | :- |
|Y|Y|0, 1/3, 2/3, 1|
|Y|N|0, 1/4, 1/2, 3/4|
|N|Y|1/4, 1/2, 3/4, 1|
|N|N|1/5, 2/5, 3/5, 4/5|

<a name="chmtopic19"></a>**Colour Gradient**

The following special properties are available for Colour Gradients.

**Regions**

Specifies the number of distinct colours used to draw the gradient. If the gradient is not Stepped (see below) and you are in 8-bit mode, dithering is employed between these colours to approximate a truly smooth gradient. Increasing the number of regions thus increases the smoothness of approximation. When not in 8-bit mode, smooth gradients are drawn with real colours rather than dithering on the Viewer, so this setting is ignored in the Viewer (but still used on the layer editors, which are always 8-bit.)

**Colours**

The two colours represent the start and end colours of the gradient; additional colours are interpolated in a linear fashion according to the number of regions specified.

**Stepped**

When checked, this causes the gradient to be drawn in solid blocks of colour rather than smoothly, so it looks like a colourised greyscale.

<a name="chmtopic20"></a>**Box/Frame and Circle/Ellipse**

The following special properties are available for Boxes/Frames and Circles/Ellipses.

**Grow**

This only has an effect when the Thickness is greater than 1 pixel. If this is checked, the thick edges of the object are centered on the defining rectangle, so the overall size of the object is greater when Thickness is greater. If it is unchecked, the object is always bounded by its defining rectangle.

<a name="chmtopic21"></a>**Frequency Grating**

The following special properties are available for Frequency Gratings.

**Period**

This is the number of pixels per cycle of the grating. Note that this means grating lines do not scale up and down when the image size is changed: the same grating appears finer, relative to the card, when the card is drawn at a larger size.

**Border**

Specifies the width of solid border around gratings, in pixels or perecentage of cell width. The border is drawn in colour 2. Increasing the border size does not increase the object size; rather, it shrinks the area used by the actual grating.

<a name="chmtopic22"></a>**FreqBurst**

The following special properties are available for FreqBurst objects.

**Bars / MHz**

If 'Bars' is selected, this gives the number of bars of colour 2, which are separated by equal-sized bars of colour 1. For example if colours 1 and 2 are white and black and Bars is 3, there will be 5 regions coloured B-W-B-W-B. (This is slightly modified for sinusoidal gratings - see below).

If 'MHz' is selected, the bar spacing will be set to give this frequency, according to the line frequency specified under Card Properties. There may therefore not be a whole number of bars in the object.

When switching between Bars and MHz, the value displayed is converted approximately between units. The conversion factor depends on the card properties and the size of the object.

**Sinusoidal**

If checked, the burst is made sinusoidal (smooth variation in colour); if unchecked, solid bars are drawn as described above. If a number of Bars is specified, that exact number of oscillations is used - for solid bars the number of periods is really 0.5 less than the number of bars, so that the burst starts and ends with the same colour.

Whether the burst is square-wave or sinusoidal, colour anti-aliasing is used to improve the regularity of the bars. Sixteenth-shades are used for anti-aliasing and for generating sinusoidal sweeps when in 8-bit mode.

**Sloping Edges**

These controls allow the burst to be tapered or sloping. The 'Back' and 'Front' edges are relative to the Direction of the burst: they are colour-coded on the small preview next to the controls. The controls show the amounts by which the bottom corners are pushed in the specified Direction, as a percentage of the normal distance between them. For example setting Back to 50 and Front to -50, when Direction is rightward, pushes the bottom left corner half the width rightward and the bottom right corner half the width leftward, meaning the burst tapers to a point. If the Back and Front settings are 0, an ordinary rectangle results; if they are equal but not 0, this gives a uniform slope (as seen on the Telefunken T05 for example). If the Direction is changed, different edges are used as Back and Front (try experimenting with these controls to get the feel of it).

<a name="chmtopic23"></a>**StarBurst**

The following special properties are available for StarBursts.

**Circular Burst**

If this is checked, the object is drawn with a circular or elliptical border, otherwise the border is square or rectangular (the exact shape depending on the Size). For elliptical bursts, the bars are squashed or stretched in proportion to the ellipse; this does not happen for rectangular bursts.

**Bars**

This gives the number of bars of each colour; the burst is drawn with alternating bars of colour 1 and colour 2, with rudimentary anti-aliasing similar to that used for FreqBursts.

**Offset %**

This rotates the position of the bars by the given percentage of the bar size. Range is -100 to +100.

<a name="chmtopic24"></a>**Sweep**

The following special properties are available for Sweep objects.

**Freq, MHz**

Two frequencies are required here, to give the start and end frequency of the sweep. If the values are the same, the sweep looks just like a FreqBurst at that frequency and without tapered edges. Otherwise, the frequency changes smoothly between the two values from the start to the end of the sweep to the other (as defined by the Direction). The change is exponential, e.g. if frequencies of 1 and 4 MHz are specified, the frequency at the midpoint will be 2MHz.

**Sinusoidal**

If checked, the sweep is made sinusoidal (smooth variation in colour); if unchecked, it is a square wave (solid alternating blocks of colour).

Whether the sweep is square-wave or sinusoidal, colour anti-aliasing is used to improve the regularity of the bars. Sixteenth-shades are used for anti-aliasing and for generating sinusoidal sweeps when in 8-bit mode.

<a name="chmtopic25"></a>**Crossbar**

The following special properties are available for Crossbar objects.

**45-degree slope**

If checked, each part of the crossbar will slope at 45 degrees (as per Test Cards D, E, F); if unchecked, the parts run parallel to an 'X' drawn through the corners of the whole object (as per Test Cards C and G).

**Size**

This determines the size of each individual part, shown as length x width (with 'length' being measured in the direction of the stripes). The size of the whole object is determined only by the Position property, because crossbars are always centred in their layer.

**Regions**

Determines the number of stripes of Colour 2 within each part. The parts are filled in with Colour 1.

**Border**

Determines the thickness of solid border (in Colour 1) around the thin-striped area in each part. As with Frequency Grating, this shrinks the size of the thin stripes rather than increasing the size of the parts.

<a name="chmtopic26"></a>**Bullseye**

The following special properties are available for Bullseye objects.

**Thickness**

The thickness of the rings drawn in Colour 1 (the remaining rings are filled in with Colour 2).

**Regions**

The number of colour-1 rings. If the centre spot is visible and is not 'Filled' then the number of colour-2 rings is the same, otherwise it is one fewer.

**Centre Spot**

The 'Diam.' value gives the diameter of the centre spot as a percentage of the cell width (i.e. as per Size values). If 'Filled' is checked, the spot is drawn with colour 1 (matching the innermost colour-1 ring and turning it into a spot), otherwise it is drawn with colour 2. (The centre spot is never transparent, even when 'Filled' is unchecked.)

**Equalise**

If the line thickness is specified as a percentage of the cell width, pressing this button sets the centre spot diameter to equal the thickness of the colour-2 (filler) rings; therefore the colour-1 rings are all equally spaced. For example if the bullseye has size 1.00x1.00, 4 regions, thickness 4%, pressing this button will size the centre spot to (1.00 - 4x0.04)/7 = 0.14.

This is not a genuine property of the bullseye, just a 'helper'. Also, it is disabled when Thickness is in absolute pixels, as the image size would affect the calculation in that case.

<a name="chmtopic27"></a>**GridCross**

The following special properties are available for GridCrosses.

**Arms**

Allows some of the arms of the gridcross to be omitted. The gridcross is divided into 8 arms forming 4 L-shaped sections. The parts of the gridcross that are drawn will match those arms that are illuminated on the control.

- Click on an individual arm to switch it on or off.
- Click in a corner, or on the corner of an L, to switch both arms of the L on/off at once.
- Click in between two arms on adjacent Ls to switch both of those arms at once.

**Cross Position**

Determines whereabouts the gridcross intersection occurs (X and Y), and the width of the gap along its lines (D, for distance). The X and Y coordinates are bounded by the Size and Position, and have unchangeable fractional parts because these are fixed by the alignment of the physical grid. D is the percentage of the grid line thickness (not the cell size) which is visible between the physical grid lines. Thus, when D=1.00 the gridcross lines fit snugly against the physical gridlines; when D=0.00 the gridcross lines touch each other, overlaying the physical grid lines.

<a name="chmtopic28"></a>**Triangle**

The following special properties are available for Triangles.

**Regions**

This gives the number of triangles to draw. Where more than one region is specified, a triangle is drawn in each sub-region, with alternating directions, allowing the creation of bow-tie and diamond shapes. The first triangle according to the specified Direction also points in that direction, so e.g. for Regions = 5 a train of triangles left to right is produced as |><|><|>, and for right to left <|><|><|.

<a name="chmtopic29"></a>**LightSpots**

The following special properties are available for LightSpots objects.

**Size**

The spots are always drawn circular, so if the Size gives too wide or too thin a rectangle, they will be centred in that rectangle and sized such that the coloured spots touch either the horizontal or vertical edges.

**Spacing**

This gives the spacing between the centres of the spots, as a proportion of the spot diameter. A larger Spacing therefore forces the spots to be smaller if the Size is unaltered. If Spacing is more than 86, there will be no central white region; when Spacing is 100, the spots are just touching; for greater values the spots are separate.

**Colour**

This is the colour of the border around the spots, if one is drawn.

**Border**

Allows a border to be drawn around each spot. Any part of the border of a spot that overlaps another spot will not be drawn. The borders grow outwards from the spots, i.e. increasing the Border value does not decrease the size of the coloured parts.

<a name="chmtopic30"></a>**Text and Clock**

The following special properties are available for Text and Clock objects, which are very similar to each other in this regard.

Note that for countdown Clocks, the value is only shown in the Viewer when it is small enough (e.g. a Countdown Minute only shows when less than 10 minutes remain on the countdown). The end time or duration of countdowns is set in the Options panel.

**Size**

If TrueSizing (see below) is not used, only the height of the object determines the text size. The specified width may be exceeded by that of the text; the text is not clipped if this happens.

Even raster fonts will scale smoothly to the required Size. (A standard Windows text control can only display a raster font in integral multiples of the defined size(s) for that font.) However, if the text is drawn very large, Windows may substitute a different font. This can be overcome by using TrueSizing with a fixed base font size.

**Alignment**

Sets the alignment of the text within the defined rectangle, as indicated by the position of the cyan circle relative to the blue box on the control. The selected corner/edge/centre of the text is aligned to the corresponding point on the rectangle. Note that because text may be wider than its rectangle, aligning text to the right may actually move it to the left, and vice versa.

**Spacing** (Text only)

Sets the amount of extra spacing between each line of multi-line text, as a percentage of the text height. Changing this value affects the height of each line of text too, so that the whole text stays vertically within its box (approximately). Note that the font used may have internal space at the top and bottom, so a Spacing of 0 does not mean the text lines will be touching. You can also set a negative Spacing value to bring the lines closer together.

**Border**

Outlines the text with a border of the given thickness in colour 2. Text size is unaffected by this, i.e. the border 'grows around' the text. This may have no visible effect if Transparent is not checked.

**Text** (Text only)

The actual text to draw. The text can be multi-line if desired:

- multi-line text will be drawn smaller so as to fit all the lines into the defined rectangle
- all lines of text are justified according to the horizontal part of the Alignment.

**Type** (Clock only)

Choose a format from the list to determine whether a time, date or countdown is shown, and the way in which it is formatted.

**Delimiter** (Clock only)

Defines the short string that separates hours, minutes etc. Default is ":" for times and countdowns or "/" for dates, as shown on the Format list, but any string of up to 3 characters can be used, including spaces, and including the empty string. The entered value is repeated on a label to the right, in double-quotes, to make it more obvious if spaces are included.

**Font**

The font with which to draw the text. Bold, italic and underline attributes can be applied via the B, U and I buttons at the right.

**TrueSizing**

Resizes the text to exactly match the horizontal and/or vertical dimensions of the object. If both horizontal and vertical TrueSizing are used, the text may be squeezed or stretched to fit the box; otherwise the aspect ratio of the text is preserved. Note also that TrueSizing in either direction causes Alignment to have no effect on the text position in that direction, since it removes any gap between the text and rectangle positions in that direction. With multi-line text and horizontal TrueSizing, the widest line is used to get the text size, and the other lines are justified using the horizontal part of Alignment.

**Base Size**

If horizontal and/or vertical TrueSizing is used, this specifies a fixed font size for drawing the text. For example a small base size can be used to give a 'chunky pixels' effect to the text.

If Base Size is 0, or if TrueSizing is not used, the font size is chosen automatically.

The thickness of text borders is not affected by the Base Size. For example if Border is set to 3 pixels and the use of a small Base Size causes the text's pixels to be magnified 5 times, the border is still drawn at 3 pixels, not rounded off to 5 and not blown up to 15.

**Sample Text**

Shows sample text in the currently selected font, style and colour(s). Clicking the sample text cycles it through five different samples: the first line of the text, letters, numbers, symbols and accented letters. For Clock objects the "first line of text" is replaced by an example time or date in the selected format, using a single space as delimiter.

<a name="chmtopic31"></a>**Picture**

The following special properties are available for Picture objects.

**File**

The file from which the picture is taken. Filenames must be selected from the drop-down list or via the 'New Pic' button. The drop-down list records all the picture files you have used while the application has been running.

**New Pic**

Allows the picture to be based on a file which is not already in the File list. Brings up an 'Open' dialog from which a bitmap or JPEG file can be selected.

If the selected file is a bitmap which uses enough colours and 8-bit mode is selected, (see 'Options') you are asked whether to use Colour Cruncher on it (see Colour Cruncher section below). If you accept, and save the resulting image under a different name, that filename is used instead of the one you originally picked.

NB: Because the layer editors always use 8-bit mode, colour-washing will occur on true-colour images in the layer editors (and even on 8-bit images if they use enough colours).

**Transparent colour**

If this is checked, a colour-square appears, allowing you to choose a transparent colour - when the picture is drawn, pixels of this colour are omitted. You can click the colour-square to choose a colour as usual, or you can click the 'eyedropper' button next to it to choose a colour from the picture itself. (The picture is shown on a separate panel; click on the image to choose a colour.)

**Relative pathname**

If this is checked, the picture's filename is stored relative to the filename of the TCD itself. For example a picture "pic.bmp" in the same folder as "C:\blah\foo\bar.tcd" would be stored relatively as ".\pic.bmp" rather than "C:\blah\foo\pic.bmp". Relative pathnames make it easier to export TCD files from one computer to another, where they might be saved in a different folder.

Because Test Card Maker needs to know what a relative pathname is relative to, this option cannot be used on a new TCD that has not yet been saved as a file.

**Lock Aspect Ratio**

If this is checked, the image will not be distorted if you resize it (whether via the Properties panel or the mouse); altering one dimension causes the other to be altered in step.

<a name="chmtopic32"></a>**Cutout**

The following special properties are available for Cutouts.

**Shape**

Select the shape of the cutout from the drop-down list. The shape will be sized to fit into the bounding rectangle defined by Size, Position and Edging. The shapes available are:

- Square / rectangle
- Circle / ellipse
- Diamond
- Triangle (four different directions)

<a name="chmtopic33"></a>**Miscellaneous Tips**

The background colour in the Viewer can be changed by single-clicking the background area. However if a dithered colour is chosen, dithering will still be used to fill in the background. (This is because it does not share the colour palette of the card image.)

Although any colours can be used in a card, there is a limit of 256 different colours per card when in 8-bit mode - even if your display is set to high-colour or true-colour mode. This is generally enough, although if a card contains pictures, some fine-tuning of bitmaps with Colour Cruncher may be required for best results.

Large sloping or tapered frequency bursts can take a noticeable time to draw, and of course everything takes longer in the Viewer if you use anti-aliasing. The editor currently redraws the whole layer when an object is changed, so you may want to leave these objects until last when composing a layer. (This may not be a problem depending on the speed of your processor and graphics card.)

For colour gradients in 8-bit mode, the more similar the start and end colours are, the fewer intersitial colours (i.e. regions) are required to create a smooth effect. To see this in action, compare for example a green-to-cyan gradient with a yellow-to-blue one.

To create a greyscale with full control over the lightest and darkest shades used (e.g. 6 regions from 5% to 95% grey) use a stepped Gradient object instead of a Greyscale.

When creating sinusoidal frequency gratings, you can use Gratings or FreqBursts. Gratings have more accurate and smoothly-varying shades when in 8-bit mode, but their period is measured in pixels, so they appear relatively finer when a card is drawn larger. FreqBurst gratings keep the same frequency relative to the card, but very fine ones may not appear as smooth as Gratings. For non-sinusoidal (square wave) frequency gratings, a FreqBurst is generally better, but you could use a block-train. The example Test Card 'C' uses block-trains in the left set of gratings and FreqBursts on the right for comparison.

Use Cell % rather than Pixels to define the thickness of grids, lines and borders if you want more consistent results when drawing the card at a range of sizes. Lines and borders are always drawn at least 1 pixel wide when Cell % is used, but for an anti-aliased image the "1 pixel" is on the larger internal image, so the result is still more consistent.

Use the Edging control for precise alignment of objects relative to gridlines, in preference to small adjustments to the Position and Size.

If an error box "Could not find image file <filename>" appears, then a picture image could not be be found where it was expected to be. This can happen because TCD files contain only the names of picture files that they require, not the actual picture data. In this case you can click 'Yes' to look for the file via a standard 'open' dialog. If you click 'No', or do not select a file, the image object will not be lost, but it will be displayed as a white rectangle with a 'cross-box' and file name, in a similar fashion to that of a web browser.

When creating thumbnails, the smoothest results are obtained from a thumbnail size which is 1/2, 1/3, 1/4 etc. of the Viewer image size. For example to create a 200x150 thumbnail, the best Viewer image sizes are 400x300, 600x450 or 900x600. This also makes thumbnail creation slightly faster than for a comparable 'mismatched' size as it requires fewer calculations.

<a name="chmtopic10"></a>**Using the Viewer**

To view the card you have created, select File|Viewer from the menu or press F12. This brings up a new maximised window, the Viewer, in which draw the whole card is drawn on a single image, at a size of your choosing. First set the size and any smoothing and level controls you want, then use the Draw button to draw the card.

The **Width** and **Height** controls determine the size of the final image:

- For anamorphic images, the width is fixed at 720 and you can only change the Height.
- For non-anamorphic images, you can only change the Width manually; the Height is automatically calculated from the Width and the aspect ratio of the card.

Tick the **Anamorphic** box to draw an anamorphic image. Anamorphic images are always 720 pixels wide, and as many pixels high as would be transmitted in a TV picture. Standard heights are 576 for a 625-line system and 480 for a 525-line system, but you can select any value in a wide range. The image will be squashed or stretched to fit the chosen size exactly, so anti-aliasing is always used even if the Anti-Aliasing factor (see below) is set to 1.

The **Draw** button draws the card using the current settings. If the result is too big to fit in the Viewer, scroll bars appear so you can move around the card. There is also an 'x' button for the scroll bars, which removes them until you redraw the card at a size requiring scroll bars.

The **Smooth** and **Levels** buttons allow you to adjust the way the card is rendered - see the [Smoothness](#chmtopic34) and [Levels](#chmtopic35) sub-pages for more details.

The **Save** button allows you to save the card, at the currently-drawn size, as a bitmap (.bmp) or JPEG (.jpg) file. For 8-bit bitmaps, all the required colours set up in the palette. The filename defaults to that of the TCD file except with a .bmp or .jpg extension, but you can use a different filename if you wish. For JPEG files, you can alter the picture quality of the saved file (see "Options" section).

The **FullScrn** button (or Ctrl+F) in the Viewer causes it to go into full-screen mode, i.e. the whole screen becomes available for showing the drawn card. The image is always centered, and no scroll bars appear when the image is too big for the screen. (This allows you to simulate overscan as well as underscan.) The mouse pointer is also removed. Once in full-screen mode, pressing any key other than F5 or F6 returns the viewer to its normal mode. (F5 and F6 control tone and CD playing). If the "Click closes in full-screen mode" option is set, then clicking with the mouse when in full-screen mode will close the Viewer completely and return to the editor, otherwise mouse clicks have no effect in full-screen mode.

The **Thumb** button brings up a small window similar to the Viewer, which allows the Viewer image to be converted to a thumbnail image up to 320 pixels wide. The thumbnail is always anti-aliased (i.e. pixel colours are averaged together) in order to capture more detail of the image, which also means true colour (24-bit) is used.

- **Draw** draws the thumbnail at the selected size. A progress bar is displayed while the thumbnail is being created - this is now fairly fast, but not instant, so the progress bar shows that something is happening!
- **Save** allows you to save the thumbnail image - the thumbnail window is removed and a standard Save dialog appears, with the filename defaulted as per the Viewer plus a prefix of 'tn\_'. As with the main Viewer image, you can save the thumbnail as a bitmap (.bmp) or JPEG (.jpg) file.
- **Close** closes the Thumbmail window.

Web pages that have thumbnail images generally use JPEG format to save bandwidth. If you want to incorporate the generated thumbnail image in a Web page, it is recommended that you use JPEG format.

**8-bit versus 24-bit colour**

If you are using the '8-bit colour' option, you will still get a 24-bit image if any of the following are true:

- The image is anamorphic
- The Anti-Aliasing factor is more than 1
- Anti-Ring is switched on

Otherwise the image will be an 8-bit image, with the palette colours chosen according to the objects in the card.

<a name="chmtopic34"></a>**Smoothness Controls**

Click the **Smooth** button in the Viewer to show or hide the Smoothness controls, which appear on their own small panel. This panel can be moved around inside the Viewer if you wish, by dragging its title bar.

![](data:image/gif;base64,R0lGODlhoQBVANMEANTQyAAAgP///4CAgAAAAEBAQObj3sK9spmQfU5JPoAAAACAAICAAIAAgACAgMDAwCwAAAAAoQBVAAAE/lDISau9OOvNu/9geA1CYJ5oqq5s675wLM90rZJ2ru9878M41OQXKBGPyGQsaDIWeUanckpFMp+/aHXL5V2lTUnROQxHS2it2Hxaj7tw4nVMbtrr+PBd3cai7XGBOnN9fnd9eVhPeBSAjoKQNISAWouIl4p/hypSYJGfLV+FlZqWm4mmppqeoK0nc2WGfm6xpbZsermuuyiTvL/AKb7BxLzDxcifx8nMcSQCANHS09TV1tfY2drb3N3e3+DTA8/h5ebn6Onq2eMS6+/w8fLo7dDz9/j58/X6/f7/3vgBHEhwoMCCCBPKO6iwocNyDB/2G0exosWLGCnaAxhRYr4B/gVCihxJsqRJABv/dfR4D6QIDAlQElzJcmGBlxdipvRHsyY8lyAOCB06VOdMct8IcFNKjWk0pU6xRU0HVAIBDkQJEDVqEKm3qU2lTgPL86YAAmixCkWrVShXjl6XAiD79BpUaXT1VT2rdu1WmV3dfZ2Ldy5TtITHJiZ8GPHTw4ydss1bbe/VDUQzv1UZV5vkx3UhF67LOCxkqKdHc7PMAYHr16838+yc7fPiu5Fvh37s+LNv1dtYb8AmeyJtqZNJl15smO1u24lxL2euTfjL4nqPW5sqHTf057pT/1Ye3KxVDgbSq1eP/aP2atx1T4/v3bnh3aSTd7OeYb3/9vj0/uSTWPuZ54F6bLEHGFyCDeiZfQWG4N96ALb0noNUGdjBhAruZFyDGMazVwewlVjhPheGaM6IG5Ro4oKcgajiOgPI42F2Ms6YDk7DBXajjkBamGOQRIqYYpFIQnRkkkzut2STUGIjYJRUXjNlleJkpOWWXGpk5JBYWgOSSWSWaSZJMKpzZZgAsMjjBieCs2aYbr6ZQZzfzNnljzXVyWNmf/GpJJiVmZkmcATy5hh14VTF1gSPWpWWBlkF+qWg4mhIwaHkwbedYjSadRlfo15VKqVroVUUp+foqekEnErn6aydtqqpqZDydV4Gla6KqZxP+hlreI0xF5V4kkFo5a26/pKaK6+AunUoanhRJo2rGUw7Wm/RjaVfbvNVp+Flp56agYuxTZsao5UF+6o7Hto2HrXH4hcuOwaa6+yuGBCnbX5OEkqNsPHqNy+oAI/HbqbP8osrvyAUB5210WDb7070FSYaeeveK6WoFZTb8AUcpiexxrW2KzDDF4elmLzGgtqdouJKGmmkZ03aX8kn50dxm+5m+2s/1vqJE4JodXjpftoMPc+3H9tpQckG4BnQkx3oaPRLVFsdsNNYbi0Cuq55vdqTYb+LE9lls7oi2lXWSBDYZ6/MJkpSi7D03XwPDHffSM4JeJKCD15k4YYHiXjiWv/N+IyLPx5i5JI7SHnlHT5djjlL7XTp+eeghy766KSXbvrpqKeu+uqsaxkBADs=)

The effect of changing these settings is not immediate - you must re-draw the card afterwards for the changes to take effect.

**Anti-Aliasing**

If this control is set to 1, the card is simply drawn on the image that you see. If the value is greater than 1, the card is drawn on a hidden image which is that many times the size in each direction, and is then shrunk with anti-aliasing onto the visible image, giving a smoother, more accurately-drawn result. The scaling process used is exactly the same as for thumbnail creation. Where anti-aliasing is used, the final result is always a true-colour bitmap, even if you are using 8-bit mode.

The card is drawn simply on the image before anti-aliasing as well, partly to make the display look better and partly to get the right positions for clock and countdown objects. If any clocks or countdowns exist, they are drawn without anti-aliasing on the completed image. (This is to save time; clocks with seconds would not work if the scaling-down of their images took more than a second in total! Anti-aliasing for clocks and countdowns may be added in a future release.)

The maximum Anti-Aliasing value is 10 in general, but this is reduced depending on the final image size, such that the maximum internal image width or height is 5120 pixels. If your PC does not have enough memory to store these very large images, a warning box is displayed.

Any object or gridline thicknesses specified as a number of pixels are scaled up on the internal large image, so that their final thickness is the same regardless of the Smoothness value. This includes the periods of frequency gratings, which are always specified as a number of pixels.

**Anti-Ring**

If the box for Anti-Ring is checked, a horizontal blur is applied to the image. The "ns" value gives the minimum "rise time" in nanoseconds. This is then the minimum time allowed between zero and maximum red, green or blue values, when the image is considered as a television signal. The degree of blurring is calculated using the Line Frequency property of the card. For example, if this is 625x25, then one line of the image represents 64000 nanoseconds, so with a rise time of 250ns, the blurring ensures that it takes at least 200/64000 = 1/256 of a line to get from a black pixel to a white one (this would be 3 pixels for a 768-pixel-wide image).

A simple flat blur is used for anti-ringing, meaning that all transitions become equally blurred, even between pixels that are not at zero or maximum level. (A "smart blur", which would only affect sharp transitions and blur them symmetrically with a genuinely limited rise rate, turns out to be very difficult to do - it tends to trip up on fine gratings, making the stripes uneven in width or brightness.)

When both Anti-Aliasing and Anti-Ring are in effect, Anti-Aliasing is applied first. A progress bar is displayed while each process is being applied, as they take a noticeable time. It may also take a long time to draw the hidden large image if a high Anti-Aliasing factor is used - there is no progress bar for this at present.



<a name="chmtopic35"></a>**Level Controls**

Click the **Levels** button in the Viewer to show or hide the Level controls, which are shown on a similar type of panel to the Smoothness controls. You can move this panel around within the Viewer by dragging its title bar.

![](data:image/gif;base64,R0lGODlhkQBlANMAANTQyAAAgP///4CAgAAAAE5JPpmQfUBAQP8AAAAA/wD/AObj3sK9soAAAACAAICAACwAAAAAkQBlAAAE/lDISau9OOvNu/8gNghBaZ5oqq5s675wLM/qSN94ru+8aZukXRA46ZWGxmTvd+QhnzCkSqqs3pgBKg26dWmt4BeWWswCj5LmOVUmpbPuYBsdrrvGqKH7rDevT31ve36BhHaHKXiAFE1yjFyAfJKGjWqIlyWKf5NSkH+DZnKWoF+YVpqjn5OWoauDopWwpnZjjHCec4tvt6mtaLC7s3VYwsXGM8THysuJpczPxcnQ08IjAgDY2drb3N3e3+Dh4uPk5ebbA9bn6+zt7u/wAOkS8fX29/jh89f5/f7/6/YBHEiwYDaBBhMqtIdwocOH5hpCnEiRm8SKBdNp3Mixo8eP/iMCqsOYcMCBkyhTqlzJciUAfhFHksx4IMSHAi9F0ptJ06YHnDDLXeTpz6RPCgySKlUKVGfQcASiEsg2VVxVblfNZY1YU4LUEEsJLG16bui3q1W3elOLja3VdkYFEJgw94NSqUxzlpX5tq3fvljZuRUXt65cEGHH6o25cxzav1KpRoW8Le1kAI8xXx6sr6thwx2WiibL+Ck4qZmpYlY9VW1r1rD9cgZXmC4IA7hz5yYtlC9U1as1T956ubLwzcFRv2ZX2yuIb7zJmV0LfPlq4sG1WY+Nnbln20cpRB83vVtm6+iTG0/NPnvZ784/LJhPn/54wr5PR4a8vz9w/lkF/oicd3RFFUJ9CN6nT35E5RNXePRJZd9ivTXWYFFdQYjghKbhZ+GFDmZ41IYcOgXiPw8epduKCtLG4InxpGjTiixSKN2LML4zAEEdLvhhjvGE99xePwJppIlHJskcjko22U15TpIH0pRUctSji0VGKV1LXHbJko1SZqklYSIKaUGL30A5ZpplmikemB5euSabZoqmmJzeqPlfYN39ts5seWb4lVyoETqoBInlheeTTGp3lnt7micYgYc5B1qlFtwVlaJIOvZfWpKeNmlAbc516aUTJJoUmnk26uhf6iG3WXEAwmoZqKRaYOqghSJl56pw+rjop9WBulxq18WWrGyU/oL3Gaag0bhbsFgOC1t6zN5Ka2uoMXvcdkKJiCqm8YnJKqNiSvpae8dS55p6r74Hnq4VjHsmtWm6ahys2a1rq6Pt/Qvok/DNa+q8ApA437kW6RtvgNy1RWty22o3oLyGGmhogZcqvADD6Dg850FtHjifhAvj22q6I1tUMggeg6yNni2TbGbMKqNrbc0yziitATIfJHLLPd/2M9A5N8xyzQfx2CnT4LjZwdNQN0lz1RdejTVRWm89U9cgermSAGKrRHbZKO2MDdgXHlClRi+5/faOZM9NN5Fqh333NXzn1Hfdfgf+d9x7C254aSO7Pfji2NTN+OCEPx540jMP3S2k/vEMrI3bgiPgOQKCc/63AqQrEHrhAiSgegKHV7gzxJqXEzs2iuf0+e0I8ON4TqX3roDutV+z+vAJ6I637IHhMzsAogOAO+58N++779HfTTzxfSNOzrvF+ScrWgNe3E3wz9/eePDT935+SKlfv3rjx2+PFa6sGWvstfx6I3r5uBP+Uvq+81/73Pe+vGntXQBKz2OUAy9x1I5/5tsdANW3OwIOj3JCW1qk+sXBBSrrXw6kGwQ/J8AJlk6AFixg/DylLAW2sIMN/MYDRwg6CZrQdBVMIesMaDn/JBCGtaJY/rbRvBFWj3cTPKLwLJg91yWOfSNcH99MKMWXpBB+2ltTa/MEwD+/bRGAXtwbASfnxDkFz3afy97u+tY7NZ5xiapT4wrHdABzkM2OdSwHDzWYI6n5cQJz9JqR2CbIiRCykA85JCIXoshFlmRojkwkJCPJyElS8pECsJsmN8nJTnryk6AMpShHScpSajICADs=)

The effect of changing these settings is not immediate - you must re-draw the card afterwards for the changes to take effect.

**Black Level, White Level**

You can set the black and white levels at any value from 0 to 255, which alters the brightness and contrast of the whole image accordingly. You can even make the white level lower than the black level, which has the added effect of reversing all the colours on the test card.

**Channels**

You can also individually switch the red, green and blue components ('channels') on or off, using the three coloured buttons on the panel. The resulting colours are still adjusted to the brightness and contrast determined by the black and white levels. For example, if the black level is 20, then pure red will be shown as grey-20 if the red channel is switched off.

**Levels for Picture objects**

If the card contains Picture objects, these have to be re-rendered when you alter any of the Level controls, causing a slight delay the first time you re-draw the card with those settings.

<a name="chmtopic36"></a>**Playing Tone and CDs**

This is achieved by pressing F5 or F6 when the Viewer is in full-screen mode.

**Playing Tone**

If you have previously recorded a tone file using ToneBox (see "ToneBox" section), you can press **F5** to play the tone; pressing F5 again stops the tone if it is still playing.

**Playing a CD**

If you have an audio CD in your CD drive, press **F6** to start playing the CD. Pressing F6 again stops the CD if it is playing. (Only standard audio CDs are supported.) \
**NB** This function may not work depending on your PC's configuration (e.g. if CDs are automatically played on insertion).

You can play tone and CD at the same time if your sound card supports it and if you really want to. Tone and CD are both stopped when you exit the Viewer. (They are not stopped if you exif from full-screen mode but do not exit the Viewer.)

<a name="chmtopic37"></a>**Tools**

This section describes the items in the Tools menu. Each item has its own subsection.

**Colour Cruncher**

Accesses the Colour Cruncher tool for reducing colours in bitmaps.

**ToneBox**

Accesses the ToneBox tool for creating test tone.

**Options**

Accesses the Options panel to allow some customisation of the behaviour of Test Card Maker

<a name="chmtopic38"></a>**Colour Cruncher**

This is a tool for reducing the number of colours in bitmap images. While Test Card Maker will support 24-bit images, it displays them with a fixed palette of 245 colours when in 8-bit mode, of which some will likely be compromised by other objects in the card. It is therefore preferable, if the final test card is going to use 8-bit colour, to use images with a reduced number of colours, and whose palette is tailored to the image at hand.

Some commercial graphics packages offer tools for reducing a 24-bit image to 8-bit, but they may use up all 256 palette entries, regardless of the diversity of colours in the original image. Colour Cruncher provides finer control of the final number of colours and of how they are merged from the original colours. You can also select a region of the image rather than the whole image. The final result can be saved over the original file or to a new file.

<a name="chmtopic39"></a>**Colour Cruncher Controls**

The following controls are available on the main Colour Cruncher panel.

**File**

The bitmap file you wish to work on. If Colour Cruncher is called while loading a new Picture object, the filename is pre-selected and cannot be changed; otherwise, click on the 'open' button (yellow folder) at the right to load a bitmap. When an image is loaded, it appears in the main work area with a selection box around the entire image.

**Selection**

Allows selection of part or all of the image when performing colour reduction. Alter the four numbers to change the selection, or press the 'All' button to select the whole image. Any part of the image that is outside the selection area is discarded after performing the colour-merge.

You can also select an area of the image by dragging over it with the mouse (i.e. press left mouse button, hold and drag).

**NB** The selection box on the image is drawn \*at\* the boundaries of the selection, not around them.

![](data:image/gif;base64,R0lGODlhHAAcANMDANTQyICAgP///wAAAEBAQACAAP8AAIAAAICAAAAAgIAAgACAgMDAwAD/AP//AAAA/ywAAAAAHAAcAAAEtBDISau9QOjNu+eEJGCkFYRZqUqnKA0wHAxBHQB3uuHoCMS0oC0n2rVSP+BsiHMZe6/YkmajcHiupJRaa+o0WKRSWJ1cjz4guZsbPbPjZbkIRq9U9jspPwFa/BN8PwaEBgMUAwUFAgWHLFAvhYWOiYqMjY9Zg4QChJSKi4qOfAMGGpMvoKCjkD+dkp+qmGE+kah9qo60FYCIMRSCehXBwoGtxcA9Q8vMzTUoBNHS09TV1MgrEQA7) **Parameters**

Brings up a panel for fine-tuning of the way Colour Cruncher merges colours. (See below.) 

![](data:image/gif;base64,R0lGODlhHAAcANMDANTQyICAgP///wAAAEBAQACAAP8AAIAAAICAAAAAgIAAgACAgMDAwAD/AP//AAAA/ywAAAAAHAAcAAAEfBDISau9QOjNu+eEJGCkFYRZqUqnuKpt+pLxOGP1LTVNMeU3Xu+Hsr2EBR+rOEMql66VswIsTanMScNyxUZ3Wy0vicuCxb2nyQwo8ADdSxUcl7PhdftX4k6/5jtkf3dtajCEOgCAiYqIOjUBkZKTlJWSKASZmpucnZyMKhEAOw==) **Crunch Now**

Starts the colour-merging operation. The 'Colours Left:' display indicates the progress of the merge.

![](data:image/gif;base64,R0lGODlhHAAcANMDANTQyICAgP///wAAAEBAQACAAP8AAIAAAICAAAAAgIAAgACAgMDAwAD/AP//AAAA/ywAAAAAHAAcAAAEjxDISau9QOjNu+eEJGCkFYRZqUqnuKpt+pLxiBk4TqO2ZPi54M/EoxgOuYNSmSO6JkFlpUmpGYUW3KFahCal0yGrC1zejhOrz0zSpsmArco9fs4AdIB6ppXr4XN5f3ZXYUd+gzKGQocVexVIUWBchBZLk46Ad2+Vm3WKnpwZAaSlpqeopSgErK2ur7CvoSoRADs=) **Revert**

Reverts to the original image (or the last saved version, if you have overwritten the file).

![](data:image/gif;base64,R0lGODlhHAAcANMLANTQyICAgP///wAAAEBAQACAAP8AAIAAAICAAAAAgIAAgAD//8DAwAD/AP//AAAA/ywAAAAAHAAcAAAErRDISau9QOjNu+eEJGCkFYRZqUqnuKptKj10bd/0FI8z/XG1BAvFAzyMgkByqVQ+Es+hq/fQNJmaoFRm9F2/Ai1gN6n9NmIy9ZylCcfEMm6ejlPpuLe6i89vizULgoODT3VTfII0hAs3enaJjQ+Mhm5/cpOSlFCWcIiBmoSOlxKcipmFnFGeXAlQjKI2j4gArra3uLakLxh7vCZEAcLDxMXGwygEysvMzc7Nv7wRADs=) **Save**

Brings up a 'Save As' dialog for the merged image. You can use the same filename if you wish; this gives a standard confirmation box before saving. The merged image is always saved as an 8-bit bitmap.

**Colours Left and Status Lamp**

The merging procedure finds and merges any pair of colours closer together than a threshold value (which increases in steps), rather than continually searching for the single closest pair of colours, then merging them, then repeating. Overall, the stepped approach is much more efficient.

The Colours Left indcator shows the number of different colours remaining in the selected part of the image. While colours are being merged, the status lamp is yellow. During a 'find closest colours' phase, the lamp turns red, and the number Colours Left stops decreasing.

When the merge is complete, the status lamp turns green.



<a name="chmtopic40"></a>**Merge Parameters**

Access this panel by clicking the Parameters (greyscale + coloured dial) button on Colour Cruncher.

The following parameters for colour merging can be changed:

**No. of Colours**

The maximum number of colours that the merged image should use. Maximum is 256, though in the context of Test Card Maker, the default value of 64 is more useful.

**Min Usage %**

Allows hardly-used colours to be merged completely into the closest colour before full colour-merging starts. The value specified here controls the threshold value below which colours will be discarded in this fashion. For example in a 200x200 pixel bitmap (40000 pixels altogether), if 0.1% is specified, colours which are used in fewer than 40 pixels will be discarded.

**Weight by Usage**

When two colours are merged (after the initial 'discard' phase) the resulting colour is in between the two. If Weight by Usage is switched on, the exact shade is determined by how many pixels used each of the two original colours, and will be closer to the more-used of the two. For example, a merge between red-200 used in 1000 pixels and red-180 used in 4000 pixels will be red-184 when weighted by usage, rather than red-190.

When Weight by Usage is off, merging is weighted by the 'merge history' of each colour, i.e. by how many original colours it is merged from. This gives the correct mean value of merged colours, no matter by what steps they were merged together.

**Black Factor**

Allows very dark colours (i.e. close to black) to be merged less discriminately. The effect of this is that more detail is lost in dark areas of the image, but more colours are thus freed for the rest of the image.

Allowed range is 0 to 100. 0 means dark colours are considered to be as far apart as medium colours. Increasing the Black Factor decreases the 'effective difference' between dark colours when deciding what to merge. For example grey-10 and grey-20 may be considered as being only as far apart as grey-128 and grey-131.

**White Factor**

Works in the same way as Black Factor but for very light colours (i.e. close to white).

**Black Reach**

An additional method for squeezing out dark colours. Any colours closer to black than the Black Reach value will be set to black. Distance to black is based on the luminosity of the colours, i.e. 2/17 blue + 5/17 red + 10/17 green, but the exact threshold value depends on the Black/White Factor parameters. This discard phase also occurs before the main merge starts.

**White Reach**

As per Black Reach, but applies to light colours, setting them to white.

<a name="chmtopic41"></a>**ToneBox**

This is a simple tool for the creation of test tone in a WAV file, which can then be played over the test card in the Viewer.

The controls are as follows:

**Pitch (Hz)**

Specifies the pitch of the tone in Hertz (cycles per second). The most commonly used values are 400, 440, 900 and 1000, but any value from 20 to 10000 is allowed here.

**Length (sec)**

Specifies the length of the tone in seconds. Range is 1 to 600 (10 minutes).

**Simple / Antiphase**

If the Simple radio-button is selected, a simple pure tone is produced. If the Antiphase box is checked, the left and right signals are inverted with respect to each other (i.e. a pure stereo-difference signal); if not, the two channels are in phase (plain mono tone.)

**GLITS** / **t=** / **P=**

If the GLITS radio-button is checked, stereo GLITS tone will be generated with a characteristic time given by the "t=" value (in seconds), with the cycle repeating after P periods of this time. The range of 't' is 0.1 to 2 seconds, with a precision of 0.01 seconds. The range of P is 5 to 99. (Cannot have P < 5 because it takes 5 periods to create the GLITS sequence.)

The GLITS cycle follows the original BBC specification, with the left channel silent in the first period and the right channel silent in the 3rd and 5th. Orignally the BBC used P=10 and t=0.6 approx, but other versions have since been used by the BBC.

**Dual / R=**

If the Dual radio-button is checked, a different frequency of pure tone is produced on each channel. The left channel uses the main Pitch value, and the right channel uses the 'R=' value.

**Volume**

Use this knob control to set the output volume. The control is logarithmic with each mark representing about 3dB of amplitude (6dB power); the maximum setting gives the largest possible amplitude in a WAV file without distortion, although it may be distorted by loudspeakers.

You can turn the knob by clicking/dragging with the mouse, or when it is the active control (the indent and markers are illuminated), use the up arrow, right arrow, '+' or ']' keys to increase the value and the down arrow, left arrow, '-' or '[' keys to decrease it.

The sample rate of the WAV file is determined from the pitch, to keep the file size down when a lower sample rate will still give a good tone. The tone file is saved as "oo.wav" in your PC's temporary directory. It is not removed when you exit Test Card Maker, so the same tone file is immediately usable the next time you start the application.

<a name="chmtopic42"></a>**Options**

This section describes the controls available on the Options panel. The controls are arranged on four tabbed pages within the panel.

**General -** Miscellaneous options

**File history shows latest** [N] **entries**

Determines the maximum number of recently-used TCDs that will be listed in the File menu. The maximum is 20. This can also be set to 0 to hide the file history if you want.

**Default to new blank TCD on startup**

If this option is checked, then when you start the application, a default TCD is created when you start the application (unless you start it by opening an existing TCD file), as per previous versions of Test Card Maker. If you then open an existing TCD without saving or editing the default TCD, the default TCD is automatically closed first.

**Editor -** Options related to the functioning of layer editors.

**Show co-ordinates of logical grid**

If this option is checked, each layer editor incorporates X and Y coordinate axes around its edges. These are tied to the logical rather than physical grid because the logical grid is used to specify object positions. This option does not affect the Viewer, in which coordinate labels are never shown.

**Show dotted lines for hidden grids**

If this option is checked, then when a layer does not have a visible grid, dotted lines are used to show the position of the logical grid, as an aid to positioning and sizing objects. The dotted lines are always 1 pixel thick and are unaffected by the layer's Centering property. They are not shown in the Viewer.

**Ask about Colour Cruncher if image uses more than** [N] **colours**

This affects whether you will be asked about using Colour Cruncher when selecting a new picture to use as a pictureThe test is applied only to 8-bit images; for 24-bit images you always get the option to use -object. Colour Cruncher when in mode. Allowed values are 0 to 255 (0 effectively means 'always ask'). For 8-bit inused by the image is checked (an 8-bit image may not use -between values, the number of colours actually all 256 colours in its palette).

This setting is ignored when the Viewer is not in 8-bit mode (see "Viewer" below). However, you can always invoke Colour Cruncher from the Tools menu, regardless of this setting and even when not in 8-bit mode.

**X-Button Action**

Determines the action of the standard Windows 'X' (close) button on the layer editors.

- Do nothing: effectively disables the X button as per previous versions of Test Card Maker.
- Close card: closes \*all\* editors associated with that TCD file, with a prompt to save changes first, as per the File|Close menu option.
- Delete layer: deletes the layer whose editor you are closing, with a confirmation box, as per the Layer|Remove menu option.



**Viewer -** Options specific to the operation of the Viewer.

**Startup Mode**

Click a radio-button to determine what happens when you invoke the Viewer:

- **Blank**: Viewer does not draw the card automatically.
- **Drawn**: Viewer draws the card automatically but does not go into full-screen mode.
- **Full**: Viewer draws the card automatically and then goes into full-screen mode.

**8-Bit Mode**

If this is option checked, all drawing in the Viewer is restricted to 256 colours as per previous versions (except when using Smoothing or Anamorphic settings in the Viewer, which always use true-colour drawing). If it is unchecked, true-colour (24-bit) drawing is used in the Viewer. Layer editors always use 8-bit mode though.

**Click closes in full-screen mode**

If this is option checked, clicking with the mouse when in full-screen mode will close the Viewer completely and return to the editor. If it is uncheked, mouse clicks have no effect in full-screen mode.

**CD Player drive letter**

Set this to the drive letter which corresponds to your CD player. (You can check which drive to use using Windows Explorer.) If this is set incorrectly, attempting to play a CD will give an error box with a message to that effect.

**JPEG save quality**

This affects the way JPEG images are saved in the Viewer. JPEG files use data compression to reduce the file size, but lose some information in the process, producing artefacts in the image (usually blocks and stripes around sharp edges). The higher this value is set, the less compression is applied when saving the file, giving a more faithful rendition but with a larger file size. Default is 80; range is 1 to 100. (When you save a JPEG file, you do not see this file on the screen, so the artefacts do not appear in the Viewer.)

**Clocks -** Options specific to Clock objects.

**Time Offset**

Click a radio-button to determine the kind of offset applied to the time on clocks:

- **None** : uses genuine local time.
- **Fixed offset**: adds or subtracts hours and minutes to local time.
- **Fixed start** : clocks start from a specified time when the card is drawn in the Viewer.

**Hours / Minutes**

Specifies the amount of offset for 'Fixed offset' or the start time (24-hour clock) for 'Fixed start'.

**Countdown**

Click the **Time of day** radio-button to count down to a fixed time of day; click the **Fixed interval** radio-button to count down through a specified amount of time.

**Time / Interval**

Specifies the fixed time (as HH:MM using the 24 hour clock) or length of time (in minutes) for the countdown, according to its Type. Where 'Fixed interval' is checked, The fixed interval starts or restarts when the card is drawn in the Viewer.

**Play tone at zero**

If this is checked, and a test card has a countdown clock, and a tone file has been created, this option causes the tone to play automatically when the countdown reaches zero (provided the Viewer is in full-screen mode at that time). If a CD was started from within Test Card Maker, it is stopped when the tone starts.
