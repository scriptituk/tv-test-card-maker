

## Summary

<img src='assets/tv-test-card-maker.gif' alt='Summary' align='right'>

Accurate high-resolution and vector graphic replicas of vintage TV test patterns are hard to come by,
and those created by drawing tools cannot be altered because master files are unavailable.

This test card maker (TCM) recreates memorable TV test patterns
with a high level of empirical accuracy.
It exposes rendering parameters for adjustment
and enables custom elements – shapes, images and text – to be superimposed anywhere.

As a novel PostScript application,
TCM demonstrates precision control of vector graphic creation
and some interesting coding paradigms that add structure and adaptability.
Indeed the implementation was key to the project rationale, so the takeaway is intentionaly twofold.

Hopefully TCM may prove useful to retro TV enthusiasts and the amateur TV community,
and perhaps spark wider interest for generic pattern generation.
Aside from TV, it champions the benefits of PostScript[^1] for creating intricate graphics programmatically.

This project is dedicated to the memory of **Gordon J. King** whose technical writings inspired so many budding electronics enthusiasts – see [dedication](#in-memoriam).


Much of the nitty gritty is contained in collapsible sections revealed in the [Table of Contents](#user-content-table-of-contents).

<details open><summary>Table of Contents</summary>
<a name='table-of-contents'></a>

- [Summary](#summary)
- [Aims](#aims)
- [Implementation](#implementation)
&bull; [Overview](#user-content-overview)
- [Installing](#installing)
  - [Install&nbsp;TCM](#install-tcm)
&bull; [Install&nbsp;Ghostscript](#install-ghostscript)
&bull; [Platform details](#user-content-platform-details)
- [PostScript&nbsp;basics](#postscript-basics)
  - [Objects](#user-content-objects)
&bull; [Operators](#user-content-operators)
- [Making&nbsp;patterns](#making-patterns)
  - [Setting&nbsp;parameters](#setting-parameters)
&bull; [Size](#size)
&bull; [Template](#template)
&bull; [Examples](#examples)
- [Pattern&nbsp;templates](#pattern-templates)
&bull; [Template&nbsp;names](#template-names)
- [Compositing&nbsp;groups](#compositing-groups)
  - [Group composition](#user-content-group-composition)
- [Group&nbsp;elements](#group-elements)
  - [GTP elements](#user-content-gtp-elements)
&bull; [BBC elements](#user-content-bbc-elements)
&bull; [PCP elements](#user-content-pcp-elements)
- [Element&nbsp;arguments](#element-arguments)
  - [GTP-A arguments](#user-content-gtp-a-arguments)
&bull; [BBC-C-early arguments](#user-content-bbc-c-early-arguments)
&bull; [BBC-C arguments](#user-content-bbc-c-arguments)
&bull; [BBC-C-625 arguments](#user-content-bbc-c-625-arguments)
&bull; [BBC-D-early arguments](#user-content-bbc-d-early-arguments)
&bull; [BBC-D-improved arguments](#user-content-bbc-d-improved-arguments)
&bull; [BBC-E arguments](#user-content-bbc-e-arguments)
&bull; [BBC-F-early arguments](#user-content-bbc-f-early-arguments)
&bull; [BBC-F-optical arguments](#user-content-bbc-f-optical-arguments)
&bull; [BBC-F-electronic arguments](#user-content-bbc-f-electronic-arguments)
&bull; [Blank arguments](#user-content-blank-arguments)
- [Custom&nbsp;elements](#custom-elements)
  - [CE&nbsp;example](#ce-example)
&bull; [CE example arguments](#user-content-ce-example-arguments)
&bull; [CE example notes](#user-content-ce-example-notes)
  - [Layering&nbsp;and&nbsp;mirroring](#layering-and-mirroring)
  - [Custom&nbsp;shapes](#custom-shapes)
&bull; [Shape arguments](#user-content-shape-arguments)
  - [Custom&nbsp;images](#custom-images)
&bull; [Image arguments](#user-content-image-arguments)
  - [Custom&nbsp;text](#custom-text)
&bull; [Text arguments](#user-content-text-arguments)
- [Resolution](#resolution)
- [Aspect&nbsp;ratio](#aspect-ratio)
- [Scaling](#scaling)
  - [Time&#8209;based&nbsp;scaling](#user-content-time-based-scaling)
&bull; [Proportional&nbsp;scaling](#user-content-proportional-scaling)
- [Timing](#timing)
- [Colours](#colours)
  - [Colour arguments](#user-content-colour-arguments)
&bull; [Greyscale](#user-content-greyscale)
&bull; [RGB](#user-content-rgb)
&bull; [YUV](#user-content-yuv)
&bull; [HSL](#user-content-hsl)
&bull; [HSB](#user-content-hsb)
&bull; [Named&nbsp;colours](#user-content-named-colours)
&bull; [Chroma&nbsp;keying](#user-content-chroma-keying)
&bull; [Random&nbsp;colour](#user-content-random-colour)
&bull; [Unit&nbsp;interval&nbsp;colour&nbsp;components](#user-content-unit-interval-colour-components)
&bull; [Transparency](#user-content-transparency)
&bull; [Gradients](#user-content-gradients)
  - [Colour space](#user-content-colour-space)
- [Fonts](#fonts)
  - [Listing&nbsp;fonts](#user-content-listing-fonts)
&bull; [Adding&nbsp;fonts](#user-content-adding-fonts)
&bull; [Editing&nbsp;fonts](#user-content-editing-fonts)
&bull; [Block&#8209;inverted&nbsp;fonts](#user-content-block-inverted-fonts)
&bull; [BBC&nbsp;logo&nbsp;fonts](#user-content-bbc-logo-fonts)
- [Command&nbsp;line&nbsp;interface](#command-line-interface)
  - [Options](#options)
    - [Basic options](#user-content-basic-options)
&bull; [Environment variables](#user-content-environment-variables)
&bull; [Finding files](#user-content-finding-files)
    - [Rendering options](#user-content-rendering-options)
&bull; [Interpolation](#user-content-interpolation)
&bull; [Antialiasing](#user-content-antialiasing)
  - [Output&nbsp;formats](#output-formats)
    - [Vector formats](#user-content-vector-formats)
&bull; [PDF](#user-content-pdf)
&bull; [EPS](#user-content-eps)
&bull; [SVG](#user-content-svg)
    - [Raster formats](#user-content-raster-formats)
&bull; [PNG](#user-content-png)
&bull; [TIFF,&nbsp;BMP,&nbsp;PNM,&nbsp;JPEG](#user-content-tiff-bmp-pnm-jpeg)
&bull; [WEBM,&nbsp;GIF](#user-content-webm-gif)
    - [Video formats](#user-content-video-formats)
&bull; [H.264/AAC&nbsp;(MP4)](#user-content-h264aac-mp4)
&bull; [FFV1/PCM&nbsp;(MKV)](#user-content-ffv1pcm-mkv)
&bull; [VP9/Opus&nbsp;(WEBM)](#user-content-vp9opus-webm)
&bull; [Animated&nbsp;PNG](#user-content-animated-png)
&bull; [Animated&nbsp;GIF](#user-content-animated-gif)
- [Video&nbsp;generation](#video-generation)
  - [Static&nbsp;testcards](#static-testcards)
&bull; [Silent&nbsp;test&nbsp;card](#user-content-silent-test-card)
&bull; [Test&nbsp;card&nbsp;with&nbsp;tone](#user-content-test-card-with-tone)
&bull; [Test&nbsp;card&nbsp;with&nbsp;music](#user-content-test-card-with-music)
  - [Overlays](#overlays)
&bull; [Overlay example](#user-content-overlay-example)
&bull; [Overlay&nbsp;commands](#user-content-overlay-commands)
&bull; [Overlay&nbsp;explanation](#user-content-overlay-explanation)
  - [DVDs](#dvds)
&bull; [DVD example](#user-content-dvd-example)
&bull; [FreeCalRec601](#user-content-freecalrec601)
&bull; [VOB&nbsp;commands](#user-content-vob-commands)
&bull; [VOB&nbsp;explanation](#user-content-vob-explanation)
&bull; [Authoring&nbsp;and&nbsp;burning](#user-content-authoring-and-burning)
- [Test&nbsp;card&nbsp;sources](#test-card-sources)
  - [Originals](#originals)
&bull; [Reconstructions](#reconstructions)
- [Graphical&nbsp;user&nbsp;interface](#graphical-user-interface)
  - [FML&nbsp;Test&nbsp;Card&nbsp;Maker](#fml-test-card-maker)
&bull; [CardMaker](#user-content-cardmaker)
- [In&nbsp;memoriam](#in-memoriam)
  - [Gordon&nbsp;J.&nbsp;King](#gordon-j-king)
&bull; [Tributes](#tributes)
- [Further&nbsp;reading](#further-reading)
  - [Television&nbsp;history](#television-history)
&bull; [Technical](#technical)
&bull; [Test&nbsp;cards](#test-cards)
&bull; [Other&nbsp;test&nbsp;card&nbsp;projects](#other-test-card-projects)
&bull; [TV&nbsp;Community](#tv-community)
  - [PostScript&nbsp;links](#postscript-links)
&bull; [Useful&nbsp;tools](#useful-tools)
  - [Footnotes](#footnotes)
</details>

## Aims

- make test patterns in vector graphic and high-resolution raster formats
- ensure faithful replicas of vintage test patterns (UK test cards initially)
- accurate digitisations from reliable sources, not reconstructions
- calculated frequency gratings, sinusoidal where needed, and other timings
- show overlay animations to demonstrate authentic accuracy
- indicate replication with removable watermark
- reference original test card image sources used to model replicas
- options to alter, add content, decorate, generally customise to requirements
- options to superimpose shapes, images and styled text anywhere
- enable transparency
- be robust enough to calibrate television receivers
- clear instructions and numerous examples
- guidance for generating videos with audio and making DVDs

## Implementation

These test patterns, a.k.a. test cards, consist of graphical [elements](#group-elements)
rendered according to [arguments](#element-arguments)
and composited according to a layout [group](#compositing-groups).
Pattern [templates](#pattern-templates) are element sets that replicate historic patterns.
All element arguments can be overridden to alter element appearance,
and additional [custom elements](#custom-elements) can be layered on top.

Patterns are created programmatically in
[PostScript](https://en.wikipedia.org/wiki/PostScript) (PS)
and generated on the command-line by [Ghostscript](https://www.ghostscript.com/) (GS).
Commands simply involve passing arguments to templates following [examples](#making-patterns) in this README.

<details><summary>Overview</summary>
<a name='overview'></a>


PostScript is an interpreted Page Description Language[^2],
somewhat underappreciated now but arguably the most concise language for computed drawing tasks like this.
Being quite vintage itself[^3], it is particularly apt for making vintage test card replicas.
Apart from its formidable control over layout and detail, it is tremendous fun!

PostScript has a rich set of graphics capabilities that accomplish the TCM [aims](#aims) in a user-centric way with minimal code.
For instance the BBC pattern graticule, corner stripes, castellations and non-sinusoidal frequency bars are all simple dashed lines, albeit wide, accomplished with the `setdash` and `lineto` PS operators.
Matrix transformations are used extensively,
for instance the corner stripes are rotated to vertical then drawn horizontally,
mirrored in the other three quadrants by reflection and translation.
Gradient and sinusoidal fills use PS shading functions.
Image imports delegate to Anastigmatix resources[^4].

Ghostscript is an open source cross-platform PostScript interpreter.
It can output high-resolution vector and raster formats
which can be post-processed to create even more image and video formats.
The command-line interface (CLI) for TCM is the GS CLI,
and the PS code uses GS-specific procedures,
therefore other interpreters will not work without modification.

This implementation makes it easy without PS or GS expertise to modify pattern [elements](#group-elements) just by changing [arguments](#element-arguments) that control composition:
dimensions, coordinates, colours, text, frequencies, imported resources, etc.
Arguments can be specified as command line options or read from file,
and follow basic PS dictionary syntax.
To achieve this in a structured way without the benefits of object-oriented features[^5] a simple argument inheritance paradigm has been devised.

Custom elements, namely [custom shapes](#custom-shapes), [custom images](#custom-images) and [custom text](#custom-text),
are a major design feature which enable graphic shapes, images, EPS[^6] vector graphics and text objects to be placed anywhere,
each with comprehensive formatting options, in ordered layers.
For instance, captions are custom-text elements and the Carole Hersee photo is a custom-image element.


</details>

> [!NOTE]
> This nomenclature of elements, arguments and groups is TCM-specific.

## Installing

### Install TCM

Click the GitHub green <kbd>Code</kbd> button at the top of the page, then <kbd>Download ZIP</kbd>.
Unzip and copy `tcm.ps` and `Resource/` to a designated TCM directory.

### Install Ghostscript

The Ghostscript interpreter is available for most platforms:

<details><summary>Platform details</summary>
<a name='platform-details'></a>


For native Windows, run the 64-bit AGPL release from [GS Downloads](https://ghostscript.com/releases/gsdnld.html)
and restart to update `%PATH%`\
(WSL and MSYS2 are good alternatives)

For ArchLinux and [MSYS2](https://www.msys2.org/), use Pacman\
e.g. `pacman -S mingw-w64-ucrt-x86_64-ghostscript` for Windows MSYS2

For Debian/Ubuntu and WSL, use APT\
e.g. `sudo apt-get install ghostscript`

For RPM-based Linux, use YUM\
e.g. `yum install ghostscript`

For Mac, use [MacPorts](https://www.macports.org/) (recommended) or [Homebrew](https://brew.sh/)\
e.g. `sudo port install ghostscript` for MacPorts

Further info: [GS User Guide: Installing](https://ghostscript.readthedocs.io/en/latest/Install.html)

</details>

## PostScript basics

All you need to grasp to tweak TCM patterns are the [objects](#user-content-objects) and [operators](#user-content-operators) detailed below and three basic concepts:

- PostScript uses *postfix* notation, a.k.a. Reverse Polish, where operands preceed operators –
like Forth[^7].
- PostScript is *stack-based*, where operands and intermediate results are stored on a stack
- everything is an *object* (all data and procedures, that is)
- whitespace seperates tokens and % begins a comment (to end of line)


The following tables show basic object types and operators needed to modify test cards.
They are mostly intuitive and by no means exhaustive
but you really shouldn’t need to dig any further.
Many of the examples take [element arguments](#element-arguments) as operands,
see for instance the [`BBC-C`](#user-content-bbc-c-arguments) set.

<details><summary>Objects</summary>
<a name='objects'></a>


| type | examples | comment |
| :--- | :--- | :--- |
| boolean | `true` `false` | these are keywords |
| numeric | `1` `-2.3` `4.5e3` | integers and reals |
| string | `(Hello)` | enclose text in `(` and `)` |
| name | `/TCh` <br> `TCh 4 div` <br> `/CCf?` | names have a slash `/` <br> drop the `/` to get named objects <br> names can have any characters |
| array | `[]` <br> `[ 1 2 3 ]` <br> `[ true 4.5 (Hi) /Lo [6 7] ]` | empty array <br> array of numbers <br> array of mixed objects |
| dictionary | `/Is? true def` <br> `/Value 8.9 def` <br> `/Text (Bye) def` <br> `/Colour /Red def` <br> `/Numbers [1 2 3] def` | these are name-object pairs <br> `def` is the *define* operator |
| null | `null` | empty or missing value |
| procedure | `{ 2 sqrt }` | an executable array of tokens |

Further info: [PLRM §3.3: Data Types and Objects](https://www.adobe.com/jp/print/postscript/pdfs/PLRM.pdf#page=48)

</details>

<details><summary>Operators</summary>
<a name='operators'></a>


| operator | example | comment |
| ---: | :---: | :--- |
| <code>_num<sub>1</sub>_ _num<sub>2</sub>_ **add** _sum_</code> | <code>1.2 3.4 **add**</code> | return <code>_num<sub>1</sub>_ + _num<sub>2</sub>_</code> |
| <code>_num<sub>1</sub>_ _num<sub>2</sub>_ **sub** _difference_</code> | <code>9.8 7.6 **sub**</code> | return <code>_num<sub>1</sub>_ - _num<sub>2</sub>_</code> |
| <code>_num<sub>1</sub>_ _num<sub>2</sub>_ **mul** _product_</code> | <code>0.5 -4 **mul**</code> | return <code>_num<sub>1</sub>_ × _num<sub>2</sub>_</code> |
| <code>_num_ **mul2** _product_</code><sup>※</sup> | <code>Gsz **mul2**</code> | return <code>_num_ × 2</code> |
| <code>_num<sub>1</sub>_ _num<sub>2</sub>_ **div** _product_</code> | <code>5.6 3 **div**</code> | return <code>_num<sub>1</sub>_ ÷ _num<sub>2</sub>_</code> |
| <code>_num_ **div2** _quotient_</code><sup>※</sup> | <code>Glw **div2**</code> | return <code>_num_ ÷ 2</code> |
| <code>_num<sub>1</sub>_ _num<sub>2</sub>_ **mod** _remainder_</code> | <code>/S7x rand TCw **mod**</code> | return remainder of <code>_num<sub>1</sub>_ ÷ _num<sub>2</sub>_</code> |
| <code>_num_ **sq** _num_</code><sup>※</sup> | <code>CCr **sq**</code> | return <code>_num_<sup>2</sup></code> |
| <code>_num_ **sqrt** _num_</code> | <code>TCy **sqrt**</code> | return <code>√<em>num</em></code> (square root) |
| <code>_num_ **neg** _num_</code> | <code>123 **neg**</code> | return <code>-_num_</code> |
| <code>_num_ **abs** _num_</code> | <code>-99 **abs**</code> | return <code>\|_num_\|</code> (absolute value) |
| <code>_leg<sub>1</sub>_ _leg<sub>2</sub>_ **hypot** _hypot_</code><sup>※</sup> | <code>TCw TCh **hypot**</code> | return hypotenuse (root sum of squares) |
| <code>_hypot_ _leg<sub>1</sub>_ **leg** _leg<sub>2</sub>_</code><sup>※</sup> | <code>Gsz mul2 Gsz **leg**</code> | return leg (cathetus, root absolute difference of squares) |
| <code>_angle_ **sin** _real_</code> | <code>-20 **sin**</code> | return sine of <code>_angle_</code> degrees |
| <code>_angle_ **cos** _real_</code> | <code>110 **cos**</code> | return cosine of <code>_angle_</code> degrees |
| <code>_angle_ **tan** _real_</code><sup>※</sup> | <code>70 **tan**</code> | return tangent of <code>_angle_</code> degrees |
| <code>_y_ _x_ **atan** _angle_</code> | <code>123 234 **atan**</code> | return arctangent of <code>_y_ ÷ _x_</code> in degrees |
| <code>_num<sub>1</sub>_ _num<sub>2</sub>_ **min** _num_</code><sup>※</sup> | <code>1.2 3.4 **min**</code> | return minimum of <code>_num<sub>1</sub>_``,``_num<sub>2</sub>_</code> |
| <code>_num<sub>1</sub>_ _num<sub>2</sub>_ **max** _num_</code><sup>※</sup> | <code>1.2 3.4 **max**</code> | return maximum of <code>_num<sub>1</sub>_``,``_num<sub>2</sub>_</code> |
| <code>_array_ **length** _int_</code> | <code>SWc **length**</code> | return length of <code>_array_</code> |
| <code>_num_ **xGsz** _product_</code><sup>※</sup> | <code>3 **xGsz**</code> | return <code>_num_ × Gsz</code> (multiply by grid size, see [scaling](#scaling)) |
| <code>– **hGsz** _size_</code><sup>※</sup> | <code>**hGsz** Glw sub</code> | return <code>Gsz ÷ 2</code> (half grid size) |
| <code>_num_ **xGlw** _product_</code><sup>※</sup> | <code>0.6 **xGlw**</code> | return <code>_num_ × Glw</code> (multiply by grid linewidth) |
| <code>– **hGlw** _width_</code><sup>※</sup> | <code>hGsz **hGlw** add</code> | return <code>Glw ÷ 2</code> (half grid linewidth) |
| <code>_freq_ **mhz** _width_</code><sup>※</sup> | <code>2.5 **mhz**</code> | return period width corresponding to MHz of active line time |
| <code>_time_ **us** _width_</code><sup>※</sup> | <code>0.25 **us**</code> | return width corresponding to μs of active line time |
| <code>_num_ **lines** _height_</code><sup>※</sup> | <code>7 **lines**</code> | return height corresponding to number of scan lines |
| <code>_left_ _bot_ _rt_ _top_ **randp** _x_ _y_</code><sup>※</sup> | <code>0 0 TCw TCh **randp**</code> | return random point within bounding box |
| <code>_any_ **cvas** _str_</code><sup>※</sup> | <code>3.14 **cvas**</code> | return number or name converted to string |
| <code>_str<sub>1</sub>_ _str<sub>2</sub>_ **cat** _str<sub>1</sub>str<sub>2</sub>_</code><sup>※</sup> | <code>(<) IDs (>) **cat** **cat**</code> | return concatenated strings |
| <code>_name_ _value_ **arg** –</code><sup>※</sup> | <code>/IDh hGsz **arg**</code> | define argument (name-object pair) iff not already defined |
| <code>_to_ _from_ **merge** –</code><sup>※</sup> | <code>/T7 /T4 **merge**</code> | define undefined args from another custom element of same type |

<sup>※</sup> TCM procedures, as opposed to built-in PS operators

Further info: [PLRM §8: Operators](https://www.adobe.com/jp/print/postscript/pdfs/PLRM.pdf#page=519)

</details>

## Making patterns

### Setting parameters

Parameters are set using [GS options](#user-content-basic-options) and [TCM arguments](#element-arguments).

### Size

The test card size parameters are `TCh` (height), `TCw` (width) and `TCr` (aspect ratio).
Two may be specified, the third is calculated,
with `TCh` & `TCw` having precedence over `TCr`, stretching horizontally.

Size parameters have to be set first to establish output dimensions that calibrate [scaling](#user-content-proportional-scaling).
They must be set using the `-d` [GS option](#user-content-basic-options).

*Examples*:

`gs -q -IResource -sDEVICE=pdfwrite -o tc.pdf -dTCh=1152 tcm.ps`\
creates a PDF 1536x1152 points (default 4:3 ratio, *BBC-F-electronic* template)

`gs -q -IResource -sDEVICE=pdfwrite -o tc.pdf -dTCw=1200 tcm.ps`\
creates a PDF 1200x900 points

`gs -q -IResource -sDEVICE=png256 -dTextAlphaBits=4 -dGraphicsAlphaBits=4 -o tc.png -dTCr=1.25 tcm.ps`\
creates a low-resolution 72dpi 8-bit indexed PNG 720x576 pixels (5:4 ratio, default 576 high)

`gs -q -IResource -sDEVICE=png16m -dTextAlphaBits=4 -dGraphicsAlphaBits=4 -r600 -dDownScaleFactor=2 -o tc.png -dTCr=1.25 -dTCw=700 -dTCh=r500 tcm.ps`\
creates a high-resolution 300dpi 24-bit PNG 2916x2083 (2083=TCh*300dpi/72ppi), `TCr` is ignored

### Template

The template `/TC` may be specified anyhow but 

### Examples

`gs -q -IResource -sDEVICE=pdfwrite -o fe.pdf tcm.ps`\
makes the default *BBC-F-electronic* pattern as a PDF file `fe.pdf`

`gs -q -IResource -sDEVICE=eps2write -o c.eps -dTC=/BBC-C tcm.ps`\
makes the long-running 405-line *BBC-C* pattern as an EPS file `c.eps`

`gs -q -IResource -sDEVICE=pnggray -dTextAlphaBits=4 -dGraphicsAlphaBits=4 -o c625.png -dTC=/BBC-C-625 tcm.ps`\
makes the 625-line *BBC-C-625* pattern as a greyscale PNG file `c625.png`

`gs -q -IResource -sDEVICE=pngalpha -o fo.png -dTC=/BBC-F-optical -dCPi=null tcm.ps`\
makes the two-slide *BBC-F-optical* pattern as a PNG file `fo.png`
with a transparent hole where the image should be (see [arguments](#user-content-bbc-f-optical-arguments))

## Pattern templates

These are the replica test card patterns composited so far.
All pattern elements can easily be adjusted or customised.

The thumbnails link to larger animated images showing replica and original overlaid, for testing.\
By default a replica icon ![](assets/icons/replica-16.svg) in the bottom-right corner watermarks the replica pattern.

<kbd align='center'>&nbsp;<br>**GTP-A**<br>&nbsp;<br>[![GTP-A](assets/templates/GTP-A-thumb.png)](assets/templates/GTP-A-anim.png)</kbd>
<kbd align='center'>&nbsp;<br>**BBC-C-early**<br>&nbsp;<br>[![BBC-C-early](assets/templates/BBC-C-early-thumb.png)](assets/templates/BBC-C-early-anim.png)</kbd>
<kbd align='center'>&nbsp;<br>**BBC-C**<br>&nbsp;<br>[![BBC-C](assets/templates/BBC-C-thumb.png)](assets/templates/BBC-C-anim.png)</kbd>
<kbd align='center'>&nbsp;<br>**BBC-D-early**<br>&nbsp;<br>[![BBC-D-early](assets/templates/BBC-D-early-thumb.png)](assets/templates/BBC-D-early-anim.png)</kbd>
<kbd align='center'>&nbsp;<br>**BBC-D-improved**<br>&nbsp;<br>[![BBC-D-improved](assets/templates/BBC-D-improved-thumb.png)](assets/templates/BBC-D-improved-anim.png)</kbd>
<kbd align='center'>&nbsp;<br>**BBC-E**<br>&nbsp;<br>[![BBC-E](assets/templates/BBC-E-thumb.png)](assets/templates/BBC-E-anim.png)</kbd>
<kbd align='center'>&nbsp;<br>**BBC-C-625**<br>&nbsp;<br>[![BBC-C-625](assets/templates/BBC-C-625-thumb.png)](assets/templates/BBC-C-625-anim.png)</kbd>
<kbd align='center'>&nbsp;<br>**BBC-F-early**<br>&nbsp;<br>[![BBC-F-early](assets/templates/BBC-F-early-thumb.png)](assets/templates/BBC-F-early-anim.png)</kbd>
<kbd align='center'>&nbsp;<br>**BBC-F-optical**<br>&nbsp;<br>[![BBC-F-optical](assets/templates/BBC-F-optical-thumb.png)](assets/templates/BBC-F-optical-anim.png)</kbd>
<kbd align='center'>&nbsp;<br>**BBC-F-electronic**<br>&nbsp;<br>[![BBC-F-electronic](assets/templates/BBC-F-electronic-thumb.png)](assets/templates/BBC-F-electronic-anim.png)</kbd>


International and widescreen patterns may follow if called for
but many modern digital test patterns exist already.

### Template names

Names are hyphenated as *group*-*designation*-*variant* which controls compositing and drawing algorithms.
The optional *variant* controls element variations.

<!-- For instance there are two test patterns deignated `G`: a Philips circle pattern[^8] used by the BBC and a classic BBC style used internationally. -->


## Compositing groups

> [!NOTE]
> Groups are of no concern unless you are coding new elements.

A compositing group is a set of visibly similar templates that share a common layout of graphic [elements](#group-elements) and their respective [arguments](#element-arguments).
Each group has its own procedure resource for compositing all patterns in the group.
Grouping enables TCM to generate widely differing patterns and provides extensibility.

<details><summary>Group composition</summary>
<a name='group-composition'></a>


| group | patterns |
| :---: | :--- |
| `/BBC` |  classic BBC/ITA/IBA/BREMA letter designation patterns |
| `/PCP` |  Philips circle patterns |
| `/GTP` |  general test patterns |

</details>

## Group elements

These are graphic elements that make up the test patterns in a group,
such as the graticule, streak box, step wedge, corner stripes, etc.

<details><summary><code>GTP</code> elements</summary>
<a name='gtp-elements'></a>

</details>

<details><summary><code>BBC</code> elements</summary>
<a name='bbc-elements'></a>

</details>

<details><summary><code>PCP</code> elements</summary>
<a name='pcp-elements'></a>

</details>

## Element arguments

These variables follow a naming convention where upper-case letters denote the element
and lower-case letters denote the parameter,
for instance `TCbc` is the test card background colour and `SWw` is the step wedge width.
A question mark denotes a switch, for instance `PP?` controls whether pulse panes are drawn.

The following tables show element arguments for each template and the hierarchy for inherited arguments.

<details><summary><code>GTP-A</code> arguments</summary>
<a name='gtp-a-arguments'></a>

Inheritance: `GTP-A` <— [`Blank`](#user-content-blank-arguments)
| arg | value | description |
| ---: | :---: | :--- |
| ***/TC…*** |  | ***test card arguments*** |
| `/TCbc` | `/white` | background colour |
| ***/G…*** | ![graticule](assets/elements/GTP-A-G.png) | ***graticule arguments*** |
| `/Gszv` | `TCh 16.5 div` | vertical grid size |
| `/Gsz` | `TCw 20.5 div 1.1 Gszv mul min 0.9 Gszv mul max` | grid size: datum for all measurements |
| ***/SB…*** | ![streak box](assets/elements/GTP-A-SB.png) | ***streak box arguments*** |
| `/SBiw` | `3 xGsz` | streak box inner width |
| `/SBih` | `0.51 xGsz` | streak box inner height |
| `/SBy` | `TCy 4.44 xGsz sub` | streak box vertical centre |
| `/SBc` | `/black` | streak box colours: [inner outer] |
| ***/CC…*** | ![centre circles](assets/elements/GTP-A-CC.png) | ***centre circles arguments*** |
| `/CClw` | `0.74 xGsz` | centre circles stroke width |
| `/CCr` | `2.6 xGsz` | white circle stroke radius |
| ***/ID…*** | ![ident designation](assets/elements/GTP-A-ID.png) | ***ident designation arguments*** |
| `/IDs` | `(A)` | ident string: empty for no ident |
| `/IDf` | `/GillSans-alt` | ident font |
| `/IDc` | `/black` | ident colour |
| `/IDh` | `0.89 xGsz` | ident height |
| `/IDx` | `TCx` | ident horizontal centre |
| `/IDy` | `TCy 5.51 xGsz sub` | ident vertical centre |
| ***/FB…*** | ![frequency bars](assets/elements/GTP-A-FB.png) | ***frequency bars arguments*** |
| `/FBh` | `SBiw` | freq bars height |
| `/FBc` | `/black` | freq bars colours: [min max surround] |
| `/FBx` | `TCx 4.81 xGsz sub` | freq bars horizontal centre |
| `/FBf` | `[ [1 6 -1 /T-2 1] [1.5 6 1 /T-3 1] [2 6 -1 /T-4 -1] [2.5 6 0 /T-1 0] [3 6 1 /T-5 -1] ]` | frequencies: [MHz nbars antiphase] array |
| ***/NP…*** |  | ***needle pulse line arguments*** |
| `/NPh` | `FBh` | needle pulse line height |
| `/NPx` | `TCx 5.91 xGsz sub` | needle pulse line horizontal centre |
| `/NPc` | `/black` |  |
| ***/B…*** | ![border](assets/elements/GTP-A-B.png) | ***border arguments*** |
| `/Bw` | `0.53 xGsz` | border width |
</details>

<details><summary><code>BBC-C-early</code> arguments</summary>
<a name='bbc-c-early-arguments'></a>

Inheritance: `BBC-C-early` <— [`Blank`](#user-content-blank-arguments)
| arg | value | description |
| ---: | :---: | :--- |
| ***/TC…*** |  | ***test card arguments*** |
| `/TCbc` | `0.6` | background colour |
| ***/G…*** | ![graticule](assets/elements/BBC-C-early-G.png) | ***graticule arguments*** |
| `/Gsz` | `TCh 0.129 mul` | grid size: datum for all measurements |
| `/Glw` | `Gsz 12 div` | grid linewidth |
| `/Golw` | `0` | grid outline width: 0 for no outline (F/J/W/X pattern) |
| `/Gps?` | `false` | true to shift grid phase by half a square |
| `/Glc` | `/white` | grid line colour |
| `/G?` | `true` | false for no graticule |
| ***/SB…*** | ![streak box](assets/elements/BBC-C-early-SB.png) | ***streak box arguments*** |
| `/SBow` | `2.66 xGsz` | streak box outer width |
| `/SBoh` | `0.89 xGsz` | streak box outer height |
| `/SBiw` | `1.75 xGsz` | streak box inner width |
| `/SBih` | `0.31 xGsz` | streak box inner height |
| `/SBy` | `TCy 2.81 xGsz add` | streak box vertical centre |
| `/SBc` | `[/black /white]` | streak box colours: [inner outer] |
| `/SB?` | `true` | false for no streak box |
| ***/PP…*** | ![pulse pane](assets/elements/BBC-C-early-PP.png) | ***pulse pane arguments*** |
| `/PPw` | `2 xGsz Glw add` | pulse pane width |
| `/PPh` | `3 xGsz Glw add` | pulse pane height |
| `/PPx` | `TCx 2 xGsz sub` | pulse pane horizontal centre |
| `/PPc` | `[/black /white]` | pulse pane colours: [left right] |
| `/PP?` | `true` | false for no pulse panes or needle pulse lines |
| ***/NP…*** |  | ***needle pulse line arguments*** |
| `/NPw` | `0.25 us` | needle pulse linewidth |
| `/NPh` | `1.8 xGsz` | needle pulse line height |
| `/NPx` | `PPx 0.725 xGsz sub` | needle pulse line horizontal centre |
| ***/ID…*** | ![ident designation](assets/elements/BBC-C-early-ID.png) | ***ident designation arguments*** |
| `/IDs` | `(C)` | ident string: empty for no ident |
| `/IDf` | `/GillSans` | ident font |
| `/IDc` | `/white` | ident colour |
| `/IDh` | `0.63 xGsz` | ident height |
| `/IDx` | `TCx 0.07 xGsz sub` | ident horizontal centre |
| `/IDy` | `TCy 3 xGsz sub` | ident vertical centre |
| `/IDdr` | `0` | ident adjacent dot radius: 0 for none |
| ***/C…*** |  | ***caption arguments*** |
| `/Ct` | `[]` | caption custom text element names: empty for no caption |
| `/Cy` | `TCy 3 xGsz sub` | caption vertical centre |
| `/Cr` | `1` | caption rectangle graticule rows |
| `/Cc` | `2` | caption rectangle graticule columns |
| `/Cch` | `1` | caption rectangle clip height scale factor |
| ***/CC…*** | ![centre circles](assets/elements/BBC-C-early-CC.png) | ***centre circles arguments*** |
| `/CCf?` | `true` | false for no fill (empty) |
| `/CClw` | `0.1 xGsz` | centre circles stroke width |
| `/CCr` | `2 xGsz` | white circle stroke radius |
| `/CCbr` | `CCr CClw add` | black circle stroke radius: 0 for none |
| `/CCor` | `CCr CClw mul2 add` | outer circle stroke radius: 0 for none |
| `/CC?` | `true` | false for no circles |
| ***/CP…*** |  | ***centre picture arguments*** |
| `/CPi` | `null` | picture custom image element name, null for no image |
| ***/SW…*** | ![step wedge](assets/elements/BBC-C-early-SW.png) | ***step wedge arguments*** |
| `/SWx` | `TCx` | step wedge horizontal centre |
| `/SWw` | `0.5 xGsz` | step wedge width |
| `/SWoh` | `2.5 xGsz` | step wedge outer height |
| `/SWc` | `[0 0.3 0.5 0.7 1]` | step wedge colours: [bottom to top] |
| `/SWds` | `0` | step wedge dot size 0 for none, diameter or [width height] array |
| `/SWdc` | `[0.2 1]` | step wedge dot colours: [bottom top] |
| `/SW?` | `true` | false for no step wedge |
| ***/FB…*** | ![frequency bars](assets/elements/BBC-C-early-FB.png) | ***frequency bars arguments*** |
| `/FB2?` | `true` | true for 2 bars, false for 1 |
| `/FBoh` | `PPh` | freq bar outer height |
| `/FBow` | `SWw` | freq bar outer width |
| `/FBh` | `0.505 xGsz` | freq bars height |
| `/FBg` | `0` | freq bars gap size (>0 for D/E) |
| `/FBp` | `0.012 xGsz` | freq bars padding |
| `/FBc` | `[0 1 1]` | freq bars colours: [min max surround] |
| `/FBs?` | `false` | true for sinusoidal frequency gratings, false for square |
| `/FBx` | `TCx CCr CClw 0.4 mul sub FBoh div2 leg sub FBow div2 add` | freq bars horizontal centre |
| `/FBf` | `[ [1 4 0] [1.5 6 0] [2 8 0] [2.5 10 0] [3 12 0] ]` | frequencies: [MHz nbars antiphase] array |
| `/FBt` | `null` | custom text element name for freq text template, null for no text |
| `/FB?` | `true` | false for no frequency bars |
| ***/CS…*** | ![corner stripes](assets/elements/BBC-C-early-CS.png) | ***corner stripes arguments*** |
| `/CSa` | `1 TCr atan` | corner stripes angle from horizontal |
| `/CSol` | `3.03 xGsz` | corner stripes outer length from corner |
| `/CSow` | `Gsz` | corner stripes outer width |
| `/CShf` | `0.9` | corner stripes horizontal fundamental MHz |
| `/CSlw` | `CShf mhz div2 1 TCar atan sin mul` | corner stripes linewidth at normal aspect ratio |
| `/CSnl` | `10` | corner stripes number of lines |
| `/CSep` | `Glw` | corner stripes end padding |
| `/CSbp` | `Glw` | corner stripes border padding (clipped) |
| `/CSc` | `[/black /white]` | corner stripes colours: [grating surround] |
| `/CS?` | `true` | false for no corner stripes |
| ***/CB…*** |  | ***colour bar arguments*** |
| `/CBh` | `0` | colour bar height: 0 for no colour bars (fraction of border width) |
| `/CBc` | `[]` | colour bar colours: [left to right] |
| `/CBew` | `0` | colour bar end widths (fraction of uniform inner widths) |
| ***/B…*** | ![border](assets/elements/BBC-C-early-B.png) | ***border arguments*** |
| `/Bw` | `0.26 xGsz` | border width |
| `/Bah` | `0` | border arrow height (fraction of border width, 0 for no arrows) |
| `/Bac` | `[1 0]` | border arrow colours: [horizontal vertical] |
| `/Bcc` | `[]` | castellation colours: empty or [left-red left-blue bottom-green right-yellow top-cyan] |
| `/B?` | `true` | false for no drawn border |
</details>

<details><summary><code>BBC-C</code> arguments</summary>
<a name='bbc-c-arguments'></a>

Inheritance: `BBC-C` <— [`BBC-C-early`](#user-content-bbc-c-early-arguments) <— [`Blank`](#user-content-blank-arguments)
| arg | value | description |
| ---: | :---: | :--- |
| ***/G…*** | ![graticule](assets/elements/BBC-C-G.png) | ***graticule arguments*** |
| `/Gsz` | `TCh 0.129 mul` | grid size: datum for all measurements |
| ***/SB…*** | ![streak box](assets/elements/BBC-C-SB.png) | ***streak box arguments*** |
| `/SBih` | `0.28 xGsz` | streak box inner height |
| ***/ID…*** | ![ident designation](assets/elements/BBC-C-ID.png) | ***ident designation arguments*** |
| `/IDf` | `/TCM-BBC_C-SemiBold` | ident font |
| `/IDh` | `0.69 xGsz` | ident height |
| `/IDx` | `TCx 0.02 xGsz sub` | ident horizontal centre |
| ***/C…*** | ![caption](assets/elements/BBC-C-C.png) | ***caption arguments*** |
| `/Ct` | `[/T-1]` | caption custom text element names: empty for no caption |
| ***/SW…*** | ![step wedge](assets/elements/BBC-C-SW.png) | ***step wedge arguments*** |
| `/SWoh` | `2.55 xGsz` | step wedge outer height |
| `/SWw` | `0.52 xGsz` | step wedge width |
| ***/NP…*** |  | ***needle pulse line arguments*** |
| `/NPx` | `PPx 0.7 xGsz sub` | needle pulse line horizontal centre |
| ***/CC…*** | ![centre circles](assets/elements/BBC-C-CC.png) | ***centre circles arguments*** |
| `/CCor` | `CCr CClw 1.9 mul add` | outer circle stroke radius: 0 for none |
| ***/FB…*** | ![frequency bars](assets/elements/BBC-C-FB.png) | ***frequency bars arguments*** |
| `/FBh` | `0.53 xGsz` | freq bars height |
| `/FBp` | `0.02 xGsz` | freq bars padding |
| ***/CS…*** | ![corner stripes](assets/elements/BBC-C-CS.png) | ***corner stripes arguments*** |
| `/CSol` | `3.08 xGsz` | corner stripes outer length from corner |
| ***/B…*** | ![border](assets/elements/BBC-C-B.png) | ***border arguments*** |
| `/Bw` | `0.29 xGsz` | border width |
| `/Bah` | `0.5` | border arrow height (fraction of border width, 0 for no arrows) |
</details>

<details><summary><code>BBC-C-625</code> arguments</summary>
<a name='bbc-c-625-arguments'></a>

Inheritance: `BBC-C-625` <— [`BBC-C`](#user-content-bbc-c-arguments) <— [`BBC-C-early`](#user-content-bbc-c-early-arguments) <— [`Blank`](#user-content-blank-arguments)
| arg | value | description |
| ---: | :---: | :--- |
| ***/TC…*** |  | ***test card arguments*** |
| `/TCbc` | `0.53` | background colour |
| ***/G…*** | ![graticule](assets/elements/BBC-C-625-G.png) | ***graticule arguments*** |
| `/Gsz` | `TCh 7.79 div` | grid size: datum for all measurements |
| `/Glw` | `Gsz 12 div` | grid linewidth |
| ***/SB…*** | ![streak box](assets/elements/BBC-C-625-SB.png) | ***streak box arguments*** |
| `/SBy` | `TCy 2.8 xGsz add` | streak box vertical centre |
| `/SBoh` | `0.89 xGsz` | streak box outer height |
| `/SBow` | `2.68 xGsz` | streak box outer width |
| ***/NP…*** |  | ***needle pulse line arguments*** |
| `/NPx` | `TCx 2.74 xGsz sub` | needle pulse line horizontal centre |
| `/NPw` | `0.2 us` | needle pulse linewidth |
| ***/ID…*** |  | ***ident designation arguments*** |
| `/IDs` | `()` | ident string: empty for no ident |
| ***/C…*** | ![caption](assets/elements/BBC-C-625-C.png) | ***caption arguments*** |
| `/Cc` | `7` | caption rectangle graticule columns |
| `/Ct` | `[/T-3 /T-4]` | caption custom text element names: empty for no caption |
| ***/CC…*** | ![centre circles](assets/elements/BBC-C-625-CC.png) | ***centre circles arguments*** |
| `/CClw` | `0.12 xGsz` | centre circles stroke width |
| `/CCr` | `2.01 xGsz` | white circle stroke radius |
| `/CCbr` | `CCr CClw add` | black circle stroke radius: 0 for none |
| `/CCor` | `CCr CClw 1.8 mul add` | outer circle stroke radius: 0 for none |
| ***/SW…*** | ![step wedge](assets/elements/BBC-C-625-SW.png) | ***step wedge arguments*** |
| `/SWoh` | `2.67 xGsz` | step wedge outer height |
| `/SWw` | `0.535 xGsz` | step wedge width |
| `/SWc` | `[0 0.33 0.5 0.8 1]` | step wedge colours: [bottom to top] |
| ***/FB…*** | ![frequency bars](assets/elements/BBC-C-625-FB.png) | ***frequency bars arguments*** |
| `/FBow` | `0.6 xGsz` | freq bar outer width |
| `/FBh` | `0.525 xGsz` | freq bars height |
| `/FBg` | `0` | freq bars gap size (>0 for D/E) |
| `/FBp` | `0.023 xGsz` | freq bars padding |
| `/FBoh` | `3 xGsz Glw add` | freq bar outer height |
| `/FBx` | `TCx CCr CClw 0.1 mul sub FBoh div2 leg sub FBow div2 add` | freq bars horizontal centre |
| `/FBf` | `[ [1.5 4 0] [2.5 7 0] [3.75 10 0] [4.5 12 0] [5.25 14 0] ]` | frequencies: [MHz nbars antiphase] array |
| `/FBt` | `/T-1` | custom text element name for freq text template, null for no text |
| ***/CS…*** | ![corner stripes](assets/elements/BBC-C-625-CS.png) | ***corner stripes arguments*** |
| `/CSol` | `3.11 xGsz` | corner stripes outer length from corner |
| `/CShf` | `1.3` | corner stripes horizontal fundamental MHz |
| ***/B…*** | ![border](assets/elements/BBC-C-625-B.png) | ***border arguments*** |
| `/Bw` | `0.29 xGsz` | border width |
| `/Bah` | `1` | border arrow height (fraction of border width, 0 for no arrows) |
| ***/X…*** |  | ***extra processing arguments*** |
| `/Xsp` | `{ Mcs }` | supplementary rendering procedures |
</details>

<details><summary><code>BBC-D-early</code> arguments</summary>
<a name='bbc-d-early-arguments'></a>

Inheritance: `BBC-D-early` <— [`BBC-C-early`](#user-content-bbc-c-early-arguments) <— [`Blank`](#user-content-blank-arguments)
| arg | value | description |
| ---: | :---: | :--- |
| ***/G…*** | ![graticule](assets/elements/BBC-D-early-G.png) | ***graticule arguments*** |
| `/Gsz` | `TCh 9 div` | grid size: datum for all measurements |
| `/Glw` | `Gsz 0.1 mul` | grid linewidth |
| `/Gps?` | `true` | true to shift grid phase by half a square |
| ***/SB…*** | ![streak box](assets/elements/BBC-D-early-SB.png) | ***streak box arguments*** |
| `/SBow` | `3.45 xGsz` | streak box outer width |
| `/SBoh` | `0.9 xGsz` | streak box outer height |
| `/SBiw` | `2.2 xGsz` | streak box inner width |
| `/SBih` | `0.4 xGsz` | streak box inner height |
| `/SBy` | `TCy 3 xGsz add` | streak box vertical centre |
| ***/PP…*** | ![pulse pane](assets/elements/BBC-D-early-PP.png) | ***pulse pane arguments*** |
| `/PPw` | `Gsz Glw add` | pulse pane width |
| `/PPh` | `2.9 xGsz Glw add` | pulse pane height |
| `/PPx` | `TCx 4 xGsz sub dup Gsz lt { Gsz add } if` | pulse pane horizontal centre |
| `/PPc` | `[/white /black]` | pulse pane colours: [left right] |
| ***/NP…*** |  | ***needle pulse line arguments*** |
| `/NPw` | `0.3 us` | needle pulse linewidth |
| `/NPx` | `PPx` | needle pulse line horizontal centre |
| ***/ID…*** | ![ident designation](assets/elements/BBC-D-early-ID.png) | ***ident designation arguments*** |
| `/IDs` | `(D)` | ident string: empty for no ident |
| `/IDf` | `/GillSans` | ident font |
| `/IDh` | `0.52 xGsz` | ident height |
| `/IDy` | `TCy 2.62 xGsz sub` | ident vertical centre |
| `/IDx` | `TCx 0.02 xGsz add` | ident horizontal centre |
| ***/C…*** | ![caption](assets/elements/BBC-D-early-C.png) | ***caption arguments*** |
| `/Cy` | `TCy 3.5 xGsz sub` | caption vertical centre |
| `/Cc` | `7` | caption rectangle graticule columns |
| `/Cch` | `0.85` | caption rectangle clip height scale factor |
| `/Ct` | `[/T-1 /T-2]` | caption custom text element names: empty for no caption |
| ***/CC…*** | ![centre circles](assets/elements/BBC-D-early-CC.png) | ***centre circles arguments*** |
| `/CClw` | `0.1 xGsz` | centre circles stroke width |
| `/CCr` | `2.05 xGsz` | white circle stroke radius |
| `/CCbr` | `CCr CClw add` | black circle stroke radius: 0 for none |
| `/CCor` | `CCr CClw mul2 add` | outer circle stroke radius: 0 for none |
| ***/SW…*** | ![step wedge](assets/elements/BBC-D-early-SW.png) | ***step wedge arguments*** |
| `/SWw` | `0.593 xGsz` | step wedge width |
| `/SWoh` | `2.965 xGsz` | step wedge outer height |
| `/SWc` | `[0 0.33 0.55 0.75 0.95]` | step wedge colours: [bottom to top] |
| `/SWds` | `1.6 xGlw` | step wedge dot size 0 for none, diameter or [width height] array |
| ***/FB…*** | ![frequency bars](assets/elements/BBC-D-early-FB.png) | ***frequency bars arguments*** |
| `/FBow` | `Gsz Glw sub` | freq bar outer width |
| `/FBh` | `0.53 xGsz` | freq bars height |
| `/FBoh` | `1.8 xGsz` | freq bar outer height |
| `/FBx` | `TCx 1.58 xGsz sub FBow div2 add` | freq bars horizontal centre |
| `/FBg` | `FBoh FBh 3 mul sub div2` | freq bars gap size (>0 for D/E) |
| `/FBp` | `0.075 xGsz` | freq bars padding |
| `/FBc` | `[ 0.25 0.75 1 ]` | freq bars colours: [min max surround] |
| `/FBs?` | `true` | true for sinusoidal frequency gratings, false for square |
| `/FBf` | `[ [1 5 0] [1.5 7 1] [2 9 1] [2.5 12 0] [2.75 13 0] [3 14 0] ]` | frequencies: [MHz nbars antiphase] array |
| ***/CS…*** | ![corner stripes](assets/elements/BBC-D-early-CS.png) | ***corner stripes arguments*** |
| `/CSa` | `45` | corner stripes angle from horizontal |
| `/CSol` | `3.31 xGsz` | corner stripes outer length from corner |
| `/CSow` | `1.05 xGsz` | corner stripes outer width |
| `/CSnl` | `8` | corner stripes number of lines |
| `/CSep` | `1.2 xGlw` | corner stripes end padding |
| `/CShf` | `1.0` | corner stripes horizontal fundamental MHz |
| `/CSlw` | `CShf mhz div2 CSa sin mul` | corner stripes linewidth at normal aspect ratio |
| ***/B…*** | ![border](assets/elements/BBC-D-early-B.png) | ***border arguments*** |
| `/Bw` | `hGsz hGlw sub` | border width |
| `/Bah` | `1` | border arrow height (fraction of border width, 0 for no arrows) |
</details>

<details><summary><code>BBC-D-improved</code> arguments</summary>
<a name='bbc-d-improved-arguments'></a>

Inheritance: `BBC-D-improved` <— [`BBC-D-early`](#user-content-bbc-d-early-arguments) <— [`BBC-C-early`](#user-content-bbc-c-early-arguments) <— [`Blank`](#user-content-blank-arguments)
| arg | value | description |
| ---: | :---: | :--- |
| ***/ID…*** | ![ident designation](assets/elements/BBC-D-improved-ID.png) | ***ident designation arguments*** |
| `/IDdr` | `0.07 xGsz` | ident adjacent dot radius: 0 for none |
| ***/C…*** | ![caption](assets/elements/BBC-D-improved-C.png) | ***caption arguments*** |
| `/Ct` | `[/T-1 /T-2]` | caption custom text element names: empty for no caption |
| ***/FB…*** | ![frequency bars](assets/elements/BBC-D-improved-FB.png) | ***frequency bars arguments*** |
| `/FBc` | `[ 0.15 0.85 1 ]` | freq bars colours: [min max surround] |
</details>

<details><summary><code>BBC-E</code> arguments</summary>
<a name='bbc-e-arguments'></a>

Inheritance: `BBC-E` <— [`BBC-D-early`](#user-content-bbc-d-early-arguments) <— [`BBC-C-early`](#user-content-bbc-c-early-arguments) <— [`Blank`](#user-content-blank-arguments)
| arg | value | description |
| ---: | :---: | :--- |
| ***/TC…*** |  | ***test card arguments*** |
| `/TCbc` | `0.5` | background colour |
| ***/G…*** | ![graticule](assets/elements/BBC-E-G.png) | ***graticule arguments*** |
| `/Glw` | `7 lines` | grid linewidth |
| ***/NP…*** |  | ***needle pulse line arguments*** |
| `/NPw` | `0.2 us` | needle pulse linewidth |
| ***/ID…*** | ![ident designation](assets/elements/BBC-E-ID.png) | ***ident designation arguments*** |
| `/IDs` | `(E)` | ident string: empty for no ident |
| `/IDy` | `TCy 2.6 xGsz sub` | ident vertical centre |
| ***/SW…*** | ![step wedge](assets/elements/BBC-E-SW.png) | ***step wedge arguments*** |
| `/SWds` | `1.3 xGlw` | step wedge dot size 0 for none, diameter or [width height] array |
| ***/FB…*** | ![frequency bars](assets/elements/BBC-E-FB.png) | ***frequency bars arguments*** |
| `/FBh` | `0.55 xGsz` | freq bars height |
| `/FBc` | `[ 0.25 0.75 0.75 ]` | freq bars colours: [min max surround] |
| `/FBf` | `[ [1.5 5 0] [2.5 9 0] [3.5 11 0] [4 13 0] [4.5 15 0] [5.25 17 0] ]` | frequencies: [MHz nbars antiphase] array |
| ***/CS…*** | ![corner stripes](assets/elements/BBC-E-CS.png) | ***corner stripes arguments*** |
| `/CShf` | `1.5` | corner stripes horizontal fundamental MHz |
</details>

<details><summary><code>BBC-F-early</code> arguments</summary>
<a name='bbc-f-early-arguments'></a>

Inheritance: `BBC-F-early` <— [`BBC-E`](#user-content-bbc-e-arguments) <— [`BBC-D-early`](#user-content-bbc-d-early-arguments) <— [`BBC-C-early`](#user-content-bbc-c-early-arguments) <— [`Blank`](#user-content-blank-arguments)
| arg | value | description |
| ---: | :---: | :--- |
| ***/G…*** | ![graticule](assets/elements/BBC-F-early-G.png) | ***graticule arguments*** |
| `/Glw` | `8 lines` | grid linewidth |
| `/Golw` | `0.42 xGlw` | grid outline width: 0 for no outline (F/J/W/X pattern) |
| ***/CP…*** | ![centre picture](assets/elements/BBC-F-early-CP.png) | ***centre picture arguments*** |
| `/CPi` | `/I-1` | picture custom image element name, null for no image |
| ***/SB…*** | ![streak box](assets/elements/BBC-F-early-SB.png) | ***streak box arguments*** |
| `/SBow` | `3.45 xGsz` | streak box outer width |
| `/SBoh` | `0.9 xGsz` | streak box outer height |
| `/SBiw` | `2.1 xGsz` | streak box inner width |
| `/SBih` | `0.45 xGsz` | streak box inner height |
| ***/PP…*** | ![pulse pane](assets/elements/BBC-F-early-PP.png) | ***pulse pane arguments*** |
| `/PP?` | `false` | false for no pulse panes or needle pulse lines |
| ***/ID…*** | ![ident designation](assets/elements/BBC-F-early-ID.png) | ***ident designation arguments*** |
| `/IDs` | `(F)` | ident string: empty for no ident |
| `/IDf` | `/Helvetica-Narrow-Bold` | ident font |
| `/IDh` | `0.38 xGsz` | ident height |
| `/IDx` | `TCx` | ident horizontal centre |
| `/IDy` | `TCy 2.71 xGsz sub` | ident vertical centre |
| `/IDdr` | `0` | ident adjacent dot radius: 0 for none |
| ***/C…*** |  | ***caption arguments*** |
| `/Ct` | `[]` | caption custom text element names: empty for no caption |
| ***/CC…*** | ![centre circles](assets/elements/BBC-F-early-CC.png) | ***centre circles arguments*** |
| `/CCf?` | `false` | false for no fill (empty) |
| `/CClw` | `0.9 xGlw` | centre circles stroke width |
| `/CCr` | `2.5 xGsz 0.8 xGlw sub` | white circle stroke radius |
| `/CCbr` | `0` | black circle stroke radius: 0 for none |
| `/CCor` | `0` | outer circle stroke radius: 0 for none |
| ***/SW…*** | ![step wedge](assets/elements/BBC-F-early-SW.png) | ***step wedge arguments*** |
| `/SWw` | `Gsz Glw sub` | step wedge width |
| `/SWx` | `lGx 2 xGsz add TCx 3 xGsz sub min` | step wedge horizontal centre |
| `/SWc` | `[0 0.2 0.3 0.4 0.6 0.85]` | step wedge colours: [bottom to top] |
| `/SWoh` | `4 xGsz Glw sub` | step wedge outer height |
| `/SWds` | `1.2 xGlw` | step wedge dot size 0 for none, diameter or [width height] array |
| ***/FB…*** | ![frequency bars](assets/elements/BBC-F-early-FB.png) | ***frequency bars arguments*** |
| `/FB2?` | `false` | true for 2 bars, false for 1 |
| `/FBow` | `SWw` | freq bar outer width |
| `/FBh` | `SWoh SWc length div` | freq bars height |
| `/FBx` | `TCx SWx sub TCx add` | freq bars horizontal centre |
| `/FBg` | `0` | freq bars gap size (>0 for D/E) |
| `/FBp` | `0` | freq bars padding |
| `/FBc` | `[ 0 0.95 1 ]` | freq bars colours: [min max surround] |
| `/FBf` | `[ [1.5 6 0] [2.5 9 0] [3.5 13 0] [4 15 0] [4.5 17 0] [5.25 20 0] ]` | frequencies: [MHz nbars antiphase] array |
| `/FBs?` | `false` | true for sinusoidal frequency gratings, false for square |
| `/FBoh` | `FBh FBf length mul` | freq bar outer height |
| `/FBt` | `/T-1` | custom text element name for freq text template, null for no text |
| ***/CS…*** | ![corner stripes](assets/elements/BBC-F-early-CS.png) | ***corner stripes arguments*** |
| `/CSol` | `2.73 xGsz` | corner stripes outer length from corner |
| `/CSow` | `1.1 xGsz` | corner stripes outer width |
| `/CSep` | `Glw` | corner stripes end padding |
| ***/CB…*** |  | ***colour bar arguments*** |
| `/CBh` | `0` | colour bar height: 0 for no colour bars (fraction of border width) |
| ***/B…*** | ![border](assets/elements/BBC-F-early-B.png) | ***border arguments*** |
| `/Bac` | `[1 1]` | border arrow colours: [horizontal vertical] |
| `/Bcc` | `[ [ 250 19 30 ] [ 27 85 157 ] [ 40 107 47 ] [ 254 203 33 ] [ 17 133 222 ] ]` | castellation colours: empty or [left-red left-blue bottom-green right-yellow top-cyan] |
</details>

<details><summary><code>BBC-F-optical</code> arguments</summary>
<a name='bbc-f-optical-arguments'></a>

Inheritance: `BBC-F-optical` <— [`BBC-F-early`](#user-content-bbc-f-early-arguments) <— [`BBC-E`](#user-content-bbc-e-arguments) <— [`BBC-D-early`](#user-content-bbc-d-early-arguments) <— [`BBC-C-early`](#user-content-bbc-c-early-arguments) <— [`Blank`](#user-content-blank-arguments)
| arg | value | description |
| ---: | :---: | :--- |
| ***/G…*** | ![graticule](assets/elements/BBC-F-optical-G.png) | ***graticule arguments*** |
| `/Glw` | `7 lines` | grid linewidth |
| `/Golw` | `0.5 xGlw` | grid outline width: 0 for no outline (F/J/W/X pattern) |
| ***/ID…*** | ![ident designation](assets/elements/BBC-F-optical-ID.png) | ***ident designation arguments*** |
| `/IDy` | `TCy 2.7 xGsz sub` | ident vertical centre |
| ***/CB…*** | ![colour bar](assets/elements/BBC-F-optical-CB.png) | ***colour bar arguments*** |
| `/CBh` | `0.75` | colour bar height: 0 for no colour bars (fraction of border width) |
| `/CBew` | `0.78` | colour bar end widths (fraction of uniform inner widths) |
| `/CBc` | `[/white /yellow /cyan /green /magenta /red /blue /black]` | colour bar colours: [left to right] |
| ***/C…*** | ![caption](assets/elements/BBC-F-optical-C.png) | ***caption arguments*** |
| `/Ct` | `[/T-1 /T-2]` | caption custom text element names: empty for no caption |
| ***/SB…*** | ![streak box](assets/elements/BBC-F-optical-SB.png) | ***streak box arguments*** |
| `/SBih` | `0.4 xGsz` | streak box inner height |
| `/SBiw` | `2.23 xGsz` | streak box inner width |
| ***/CC…*** | ![centre circles](assets/elements/BBC-F-optical-CC.png) | ***centre circles arguments*** |
| `/CCr` | `2.5 xGsz 0.88 xGlw sub` | white circle stroke radius |
| ***/FB…*** | ![frequency bars](assets/elements/BBC-F-optical-FB.png) | ***frequency bars arguments*** |
| `/FBt` | `null` | custom text element name for freq text template, null for no text |
</details>

<details><summary><code>BBC-F-electronic</code> arguments</summary>
<a name='bbc-f-electronic-arguments'></a>

Inheritance: `BBC-F-electronic` <— [`BBC-F-optical`](#user-content-bbc-f-optical-arguments) <— [`BBC-F-early`](#user-content-bbc-f-early-arguments) <— [`BBC-E`](#user-content-bbc-e-arguments) <— [`BBC-D-early`](#user-content-bbc-d-early-arguments) <— [`BBC-C-early`](#user-content-bbc-c-early-arguments) <— [`Blank`](#user-content-blank-arguments)
| arg | value | description |
| ---: | :---: | :--- |
| ***/G…*** | ![graticule](assets/elements/BBC-F-electronic-G.png) | ***graticule arguments*** |
| `/Glw` | `5 lines` | grid linewidth |
| `/Golw` | `0.65 xGlw` | grid outline width: 0 for no outline (F/J/W/X pattern) |
| ***/CC…*** | ![centre circles](assets/elements/BBC-F-electronic-CC.png) | ***centre circles arguments*** |
| `/CCr` | `2.5 xGsz 1.15 xGlw sub` | white circle stroke radius |
| `/CClw` | `1.33 xGlw` | centre circles stroke width |
| ***/ID…*** | ![ident designation](assets/elements/BBC-F-electronic-ID.png) | ***ident designation arguments*** |
| `/IDf` | `/Sanchez-Regular` | ident font |
| `/IDh` | `0.39 xGsz` | ident height |
| `/IDy` | `TCy 2.71 xGsz sub` | ident vertical centre |
| ***/C…*** | ![caption](assets/elements/BBC-F-electronic-C.png) | ***caption arguments*** |
| `/Ct` | `[/T-2 /T-3]` | caption custom text element names: empty for no caption |
| `/Cch` | `1` | caption rectangle clip height scale factor |
| ***/SB…*** | ![streak box](assets/elements/BBC-F-electronic-SB.png) | ***streak box arguments*** |
| `/SBoh` | `0.87 xGsz` | streak box outer height |
| `/SBih` | `0.39 xGsz` | streak box inner height |
| `/SBiw` | `2.2 xGsz` | streak box inner width |
| ***/CB…*** | ![colour bar](assets/elements/BBC-F-electronic-CB.png) | ***colour bar arguments*** |
| `/CBh` | `1` | colour bar height: 0 for no colour bars (fraction of border width) |
| `/CBew` | `0.5` | colour bar end widths (fraction of uniform inner widths) |
| `/CBc` | `[/white /yellow /cyan /green /magenta /red /blue /black /white]` | colour bar colours: [left to right] |
| ***/SW…*** | ![step wedge](assets/elements/BBC-F-electronic-SW.png) | ***step wedge arguments*** |
| `/SWc` | `[0 47 93 139 183 232]` | step wedge colours: [bottom to top] |
| `/SWoh` | `4 xGsz Golw 3 mul sub` | step wedge outer height |
| `/SWw` | `Gsz hGlw sub Golw 1.5 mul sub` | step wedge width |
| `/SWx` | `lGx 2 xGsz add TCx 3 xGsz sub min hGsz add hGlw sub SWw div2 sub` | step wedge horizontal centre |
| `/SWds` | `[ 1.5 xGlw dup TCr div ]` | step wedge dot size 0 for none, diameter or [width height] array |
| ***/FB…*** | ![frequency bars](assets/elements/BBC-F-electronic-FB.png) | ***frequency bars arguments*** |
| `/FBf` | `[ [1.5 6 0] [2.5 10 0] [3.5 13 1] [4 15 0] [4.5 17 0] [5.25 20 0] ]` | frequencies: [MHz nbars antiphase] array |
| `/FBs?` | `true` | true for sinusoidal frequency gratings, false for square |
| `/FBt` | `null` | custom text element name for freq text template, null for no text |
| ***/CS…*** | ![corner stripes](assets/elements/BBC-F-electronic-CS.png) | ***corner stripes arguments*** |
| `/CSol` | `2.7 xGsz` | corner stripes outer length from corner |
| `/CSow` | `1.05 xGsz` | corner stripes outer width |
| `/CSep` | `1.5 xGlw` | corner stripes end padding |
| ***/B…*** | ![border](assets/elements/BBC-F-electronic-B.png) | ***border arguments*** |
| `/Bcc` | `[ [235 70 70] [70 70 235] [70 253 70] [253 253 70] [70 253 253] ]` | castellation colours: empty or [left-red left-blue bottom-green right-yellow top-cyan] |
</details>

<details><summary><code>Blank</code> arguments</summary>
<a name='blank-arguments'></a>


| arg | value | description |
| ---: | :---: | :--- |
| ***/X…*** |  | ***extra processing arguments*** |
| `/Xsp` | `{}` | supplementary rendering procedures |
| `/Xwt` | `/T-9` | watermark text element name, null for no watermark |
| `/X?` | `true` | false for no extra processing |
</details>

## Custom elements

Custom elements (CE) are
[custom shape](#custom-shapes), [custom image](#custom-images) and [custom text](#custom-text)
elements layered over the composite pattern.

CEs let you overlay your own pattern elements, such as call signs, regional information, event promotion, photos, clip art, humour etc.
With a bit of scripting you can have hundreds of CEs, positioned in an orderly fashion or at random using the `rand` [operator](#user-content-operators).

Each CE has a name formed from a type letter and an element number, e.g. `/S4` (shape 4), `/I23` (image 23), `/T17` (text 17).
CEs with a negative element number are not layered, they are for replica elements,
but they can be overridden in the normal way, for instance to change captions.

### CE example

[![custom elements](assets/ce-example-small.png)](assets/ce-example.png)

*Example*:
pattern *BBC-D-early* with 500 custom elements

Here is a 1960s-themed example to illustrate the concept (click to enlarge).
It is created from the arguments below extracted from the [args file](assets/ce-example.ps) used.
Unspecified arguments take default values –
see [shape arguments](#user-content-shape-arguments), [image arguments](#user-content-image-arguments), [text arguments](#user-content-text-arguments).

<details><summary>CE example arguments</summary>
<a name='ce-example-arguments'></a>


| arg | value | description |
| :---: | :---: | :--- |
| ***T12*** | ![T12](assets/ce/T12.png) | ***dark blue TCM title*** |
| `/T12s` | `(Test Card Maker)` | text string |
| `/T12f` | `/Times,BoldItalic` | font name |
| `/T12c` | `/MidnightBlue` | colour |
| `/T12h` | `Gsz 3 div` | height |
| `/T12y` | `TCh 0.8 xGsz sub` | horizontal centre |
| `/T12z` | `30` | z-index |
| ***S12*** | ![S12](assets/ce/S12.png) | ***sky blue filled ellipse with dark green stroke*** |
| `/S12s` | `/Ellipse` | shape |
| `/S12c` | `/LightSkyBlue` | fill colour |
| `/S12k` | `/ForestGreen` | stroke colour |
| `/S12h` | `0.6 xGsz` | height |
| `/S12w` | `5 xGsz` | width |
| `/S12y` | `T12y` | horizontal centre |
| `/S12t` | `2 lines` | stroke thickness |
| `/S12d` | `[5 xGlw Glw]` | stroke dash |
| `/S12z` | `30` | z-index |
| ***S20*** | ![S20](assets/ce/S20.png) | ***green filled Reuleaux triangles*** |
| `/S20s` | `/Polygon` | shape |
| `/S20x` | `Gsz` | horizontal centre |
| `/S20y` | `Gsz` | vertical centre |
| `/S20h` | `Gsz` | height |
| `/S20w` | `Gsz` | width |
| `/S20n` | `3` | number of sides |
| `/S20r` | `true` | Reuleaux polygon curve sides |
| `/S20a` | `15` | rotate anticlockwise |
| `/S20c` | `/Green` | fill colour |
| `/S20k` | `null` | no stroke |
| `/S20q` | `/VB` | mirror in top quadrants |
| `/S20z` | `30` | z-index |
| ***S15*** | ![S15](assets/ce/S15.png) | ***yellow stroked circle*** |
| `/S15s` | `/Circle` | shape |
| `/S15k` | `/Yellow` | stroke colour |
| `/S15c` | `null` | no fill |
| `/S15h` | `6 xGsz` | diameter |
| `/S15t` | `CClw mul2` | stroke thickness |
| `/S15z` | `10` | z-index |
| ***S14*** | ![S14](assets/ce/S14.png) | ***red stroked polygon*** |
| `/S14s` | `/Polygon` | shape |
| `/S14n` | `11` | number of sides |
| `/S14k` | `/red` | stroke colour |
| `/S14c` | `null` | no fill |
| `/S14h` | `S15h 1.01 mul` | height |
| `/S14w` | `S14h` | width |
| `/S14y` | `TCy 1.007 mul` | vertical centre |
| `/S14t` | `1 lines` | stroke thickness |
| `/S14z` | `20` | z-index |
| `/S14` | `/S15 merge` | merge in shape S15 args |
| ***I11*** | ![I11](assets/ce/I11.png) | ***PNG8: 1965 curved text*** |
| `/I11f` | `(CE/1965.png)` | image filename |
| `/I11y` | `TCy 1.2 xGsz add` | vertical centre |
| `/I11w` | `5.3 xGsz` | width |
| `/I11h` | `-1` | height |
| `/I11z` | `10` | z-index |
| ***I1*** | ![I1](assets/ce/I1.png) | ***PNG24: The Magic Roundabout*** |
| `/I1f` | `(CE/Magic-Roundabout.png)` | image filename |
| `/I1h` | `CCr mul2 CClw sub` | image diameter |
| `/I1w` | `0` | circle |
| `/I1z` | `10` | z-index |
| ***I2*** | ![I2](assets/ce/I2.png) | ***EPS: Art Nouveau by Dan X. Solo*** |
| `/I2f` | `(CE/ArtNouveauCornerOrnament-DXSolo.eps)` | image filename |
| `/I2x` | `3.25 xGsz` | horizontal centre |
| `/I2y` | `6.75 xGsz` | vertical centre |
| `/I2w` | `1.5 xGsz` | width |
| `/I2h` | `I2w` | height |
| `/I2q` | `/NHVB` | mirror in other quadrants |
| `/I2z` | `10` | z-index |
| ***T10*** | ![T10](assets/ce/T10.png) | ***blue block-inverted CE caption*** |
| `/T10s` | `(Custom Elements)` | text string |
| `/T10f` | `/Helvetica-Bold` | font name |
| `/T10h` | `0.4 xGsz` | height |
| `/T10w` | `5 xGsz` | width |
| `/T10o` | `1.2` | horizontal padding multiplier |
| `/T10y` | `Cy` | vertical centre |
| `/T10a` | `/J` | alignment |
| `/T10c` | `/Blue` | colour |
| `/T10b` | `true` | block-inverted |
| `/T10r` | `0.15` | corner radius (fraction of height) |
| `/T10z` | `10` | z-index |
| ***I4*** | ![I4](assets/ce/I4.png) | ***PNG8: Florence*** |
| `/I4f` | `(CE/Florence.png)` | image filename |
| `/I4x` | `2.9 xGsz` | horizontal centre |
| `/I4y` | `1.4 xGsz` | vertical centre |
| `/I4h` | `2.4 xGsz` | height |
| `/I4w` | `-1 xGsz` | width auto |
| `/I4z` | `31` | z-index |
| ***I5*** | ![I5](assets/ce/I5.png) | ***PNG8: Dougal*** |
| `/I5f` | `(CE/Dougal.png)` | image filename |
| `/I5x` | `1.8 xGsz` | horizontal centre |
| `/I5y` | `0.95 xGsz` | vertical centre |
| `/I5h` | `1.3 xGsz` | height |
| `/I5w` | `-1 xGsz` | width auto |
| `/I5z` | `30` | z-index |
| ***I6*** | ![I6](assets/ce/I6.png) | ***PNG8: Dylan*** |
| `/I6f` | `(CE/Dylan.png)` | image filename |
| `/I6x` | `1.2 xGsz` | horizontal centre |
| `/I6y` | `1.5 xGsz` | vertical centre |
| `/I6h` | `2.7 xGsz` | height |
| `/I6w` | `-1` | width auto |
| `/I6z` | `31` | z-index |
| ***I7*** | ![I7](assets/ce/I7.png) | ***PNG8: Ermintrude*** |
| `/I7f` | `(CE/Ermintrude.png)` | image filename |
| `/I7x` | `TCw 1.9 xGsz sub` | horizontal centre |
| `/I7y` | `1.4 xGsz` | vertical centre |
| `/I7w` | `3.8 xGsz` | width |
| `/I7h` | `-1` | height auto |
| `/I7z` | `29` | z-index |
| ***I8*** | ![I8](assets/ce/I8.png) | ***PNG8: Brian*** |
| `/I8f` | `(CE/Brian.png)` | image filename |
| `/I8x` | `TCw 1.4 xGsz sub` | horizontal centre |
| `/I8y` | `1.1 xGsz` | vertical centre |
| `/I8h` | `1.6 xGsz` | height |
| `/I8w` | `-1` | width auto |
| `/I8z` | `31` | z-index |
| ***I9*** | ![I9](assets/ce/I9.png) | ***PNG8: Zebedee*** |
| `/I9f` | `(CE/Zebedee.png)` | image filename |
| `/I9x` | `TCw 1.3 xGsz sub` | horizontal centre |
| `/I9y` | `1.9 xGsz` | vertical centre |
| `/I9h` | `1.9 xGsz` | height |
| `/I9w` | `-1 xGsz` | width auto |
| `/I9z` | `30` | z-index |
| ***S3*** | ![S3](assets/ce/S3.png) | ***dark grey stroked rectangles*** |
| `/S3s` | `/Rectangle` | shape |
| `/S3k` | `/DarkGrey` | stroke colour |
| `/S3c` | `null` | no fill |
| `/S3x` | `PPx` | horizontal centre |
| `/S3h` | `3 xGsz` | height |
| `/S3w` | `Gsz` | width |
| `/S3t` | `Glw` | stroke thickness |
| `/S3j` | `/R` | rounded corners |
| `/S3q` | `/NH` | mirror horizontally |
| `/S3z` | `20` | z-index |
| ***S5-6*** | ![S5-6](assets/ce/S5-6.png) | ***red & cyan filled triangles*** |
| `/S5s` | `/Polygon` | shape |
| `/S5n` | `3` | number of sides |
| `/S5a` | `90` | rotate anticlockwise |
| `/S5c` | `/Red` | fill colour |
| `/S5k` | `null` | no stroke |
| `/S5h` | `0.52 xGsz` | height |
| `/S5w` | `S5h` | width |
| `/S5x` | `S5w div2` | horizontal centre |
| `/S5y` | `TCy` | vertical centre |
| `/S5t` | `1 lines` | stroke thickness |
| `/S5q` | `/NH` | mirror horizontally |
| `/S5z` | `10` | z-index |
| `/S6s` | `/P` | shape |
| `/S6c` | `/Cyan` | fill colour |
| `/S6a` | `180` | rotate anticlockwise |
| `/S6x` | `TCx` | horizontal centre |
| `/S6y` | `S5x` | vertical centre |
| `/S6q` | `/NV` | mirror vertically |
| `/S6` | `/S5 merge` | merge in shape S5 args |
| ***S1*** | ![S1](assets/ce/S1.png) | ***red stroked lines*** |
| `/S1s` | `/Line` | shape |
| `/S1k` | `/Red` | stroke colour |
| `/S1c` | `null` | no fill |
| `/S1x` | `Gsz` | horizontal centre |
| `/S1h` | `Gsz` | height |
| `/S1a` | `90` | rotate anticlockwise |
| `/S1t` | `Glw` | stroke thickness |
| `/S1q` | `/NH` | mirror horizontally |
| `/S1z` | `10` | z-index |
| ***S10*** | ![S10](assets/ce/S10.png) | ***chocolate brown stroked rectangle*** |
| `/S10s` | `/Rectangle` | shape |
| `/S10k` | `/Chocolate` | stroke colour |
| `/S10c` | `null` | no fill |
| `/S10h` | `8 xGsz` | height |
| `/S10w` | `11 xGsz` | width |
| `/S10t` | `Glw` | stroke thickness |
| `/S10z` | `20` | z-index |
| ***T101-580*** | ![T101-580](assets/ce/T101-580.png) | ***border decoration*** |
| `/T#f` | `/ZapfDingbats` | font name |
| `/T#s` | a character from ``(^_`acdef)`` | random dingbat from 4 fleurons, 3 snowflakes, 1 asterisk |
| `/T#h` | `0.1 xGsz`to `0.22 xGsz` | random height |
| `/T#c` | a colour from `[/yellow /cyan /green /magenta /red /blue]` | random RGB primary or secondary colour |
| `/T#x` | from `randp` | random horizontal position within border |
| `/T#y` | from `randp` | random vertical position within border |
| `/T#z` | `0` | z-index |

(`#` is the text element number 101-580)

(other arguments that lighten the background and alter the ident are not shown)

</details>

<details><summary>CE example notes</summary>
<a name='ce-example-notes'></a>


- `T12` & `S12`(title & frame): both CEs numbered 12 but text is layered over shapes, see [layering](#layering-and-mirroring)
- `S20`(green triangles): drawn in quadrant Q3 at bottom-left but only painted in Q2 and Q1, see [mirroring](#layering-and-mirroring)
- `I2`(Art Nouveau): transparent EPS, drawn in quadrant Q2 but painted in all quadrants
- `I11`(curved text) & `I4`-`I9`(Zebedee & co.): indexed PNGs with transparency dither and matte equal to `TCbg` background colour to blend in outline and shadow effects
- `T101`-`T580`(border decoration): 480 dingbats in random colours, sizes, characters and positions generated by PS loop constructs

</details>

> ![Aside](assets/icons/aside-16.svg)\
> In 1965 Test Card D was amended and _The Magic Roundabout_ first aired,
  as did _Jackanory_, _Thunderbirds_ and _Till Death Us Do Part_.

### Layering and mirroring

Layering provides CE overlap control but is only needed when elements actually overlap, as in the example.

Each CE has an index for visual layering, like `z-index` in CSS[^9].
Lower index CEs are painted before higher ones.
CEs with identical index but different type are also layered but have a lower priority:
text (`T`) over images (`I`) over shapes (`S`).
For instance CEs with z-indices `I3z=40`, `T5z=70`, `S3z=40`, `T7z=10`
are layered `T7`, `S3`, `I3`, `T5` with `T5` on top.
Layering of CEs with identical index and same type is undefined.
Layering of mirrored CEs is described next.

<img src='assets/quadrants.png' alt='Quadrants' align='left'>

All coordinates are relative to the origin 0,0 at bottom-left in quadrant Q3.
By combining reflection and translation transformations,
custom [shapes](#custom-shapes) and [images](#custom-images) (text makes no sense)
can be mirrored as though painted relative to any corner, and get flipped over accordingly.

The mirroring argument determines which quadrant corners act as the origin:
`/N` (Q3, default) the Normal origin,
`/H` (Q4) to paint Horizontally mirrored,
`/V` (Q2) for Vertically mirrored,
`/B` (Q1) for Both horizontally and vertically mirrored.
The order of the letters determines the painting order, i.e. the layering.
For instance for `/NHBV`, a CE painted in Q3 is then mirrored in Q4 then Q1 then Q2,
but if it paints into Q2 then it mirrors into Q1 then Q4 then Q3.
Similarly `/HB` paints the horizontal and diagonally opposite reflections only,
without painting from the Q3 origin at all.


### Custom shapes

<img src='assets/Rotation_of_Reuleaux_triangle.gif' alt='Reuleaux triangle' align='right'>

Shapes are currently limited to lines, concave polygons, rectangles and ellipses, squares and circles.
They are calculated to fit the unit square[^10] at the specified rotation then scaled.
Odd-sided polygons are oriented with a vertex at top-centre and horizontal base,
placed using constant width Reuleaux[^11] curve fitting to normalise size and rotation within the bounds,
therefore the centroid is offset from the specified centre as this animation shows (credit: *LEMeZza/Wikimedia Commons*).
All shapes can be rotated and distorted, filled and/or stroked, and selectively [mirrored](#layering-and-mirroring) in all quadrants.
See also [colour arguments](#user-content-colour-arguments).

<details><summary>Shape arguments</summary>
<a name='shape-arguments'></a>


| arg | default | description |
| :---: | :---: | :--- |
| `/S#s` | `/R` | shape (required): /S(quare), /C(ircle), /L(ine), /R(ectangle), /E(llipse), /P(olygon) |
| `/S#c` | `/LightGrey` | fill colour: null for no fill |
| `/S#k` | `/DarkGrey` | stroke colour: null for no stroke |
| `/S#x` | `TCx` | horizontal centre |
| `/S#y` | `TCy` | vertical centre |
| `/S#h` | `TCh 5 div` | height/diameter/length |
| `/S#w` | `TCh 5 div` | width (ignored for Square/Circle/Line) |
| `/S#a` | `0` | rotation angle (degrees anticlockwise) |
| `/S#n` | `3` | number of sides (Polygon) |
| `/S#r` | `false` | true for Reuleaux polygon curve sides (odd-sided only) |
| `/S#d` | `[]` | stroke dash pattern: empty for solid else dash-length gap-length pairs |
| `/S#t` | `1` | stroke thickness |
| `/S#j` | `/M` | stroke line join: /M(itre), /R(ound), /B(evel) |
| `/S#q` | `/N` | mirroring: /N(one), /H(orizontal), /V(ertical), /B(oth) |
| `/S#z` | `0` | z-index for layering |
| `/S#?` | `true` | true to show this custom shape element |

(`#` is the shape element number)

</details>


### Custom images

Image import accepts JPEG, PNG, EPS and JFIF formats.
Transparency in EPS and 8-bit indexed PNG images works but 32-bit PNG images with an alpha channel are not supported.
Scaling is relative to the auto-fit scale which is calculated using offset translation, rotation and scalar projection[^12] to enclose the specified rectangle or circle.
Images are then clipped to that shape.
Unlike custom shapes and text, images cannot be distorted, but like shapes they can be selectively [mirrored](#layering-and-mirroring) in all quadrants.

<details><summary>Image arguments</summary>
<a name='image-arguments'></a>


| arg | default | description |
| :---: | :---: | :--- |
| `/I#f` | `()` | image filename (required), accepts JPEG/PNG/EPS/JFIF |
| `/I#x` | `TCx` | horizontal centre |
| `/I#y` | `TCy` | vertical centre |
| `/I#h` | `TCh 5 div` | height/diameter: -1 to calculate from aspect ratio |
| `/I#w` | `TCh 5 div` | width: 0 for circle, -1 to calculate from aspect ratio |
| `/I#a` | `0` | rotation angle (degrees anticlockwise) |
| `/I#s` | `0` | scale: 0 to auto-fit to width,height max |
| `/I#i` | `0` | horizontal offset from x at auto-fit scaling |
| `/I#j` | `0` | vertical offset from y at auto-fit scaling |
| `/I#q` | `/N` | mirroring: /N(one), /H(orizontal), /V(ertical), /B(oth) |
| `/I#z` | `0` | z-index for layering |
| `/I#?` | `true` | true to show this custom image element |

(`#` is the image element number)

> ![Tip](assets/icons/tip-16.svg)\
  To position, use auto-fit scale to centre the offset point then rotate and scale.

> ![Caution](assets/icons/caution-16.svg)\
  GS fails for EPS files with DOS/Windows line endings, so use:\
  `sed $'s/\r$//' bad.eps > good.eps` to remove CR characters.
  EPS files with Document Structuring Convention (DSC)[^13] errors can be fixed by regenerating through GS:
  `eps2eps bad.eps good.eps`


</details>

### Custom text

Text can be aligned around the compass, justified, scaled, distorted to fit width,
and block-inverted to replicate logos like ![BBC](assets/bbc.png) (sometimes called cameo fonts).
There are many arguments to control block-inversion,
including monospacing, padding, rounded corners, tracking.
See also [font resources](#user-content-font-resources) and [colour arguments](#user-content-colour-arguments).

For styled text, create it in a word processor and export to PDF,
then use the GhostScript `eps2eps` utility to convert to EPS:\
`eps2eps text.pdf text.eps`\
and render it as a [custom image](#custom-images) instead.

<details><summary>Text arguments</summary>
<a name='text-arguments'></a>


| arg | default | description |
| :---: | :---: | :--- |
| `/T#s` | `()` | text string (required); T used to size font if string has no height |
| `/T#f` | `/Helvetica` | font name |
| `/T#c` | `/Black` | colour |
| `/T#x` | `TCx` | horizontal alignment anchor |
| `/T#y` | `TCy` | vertical alignment anchor |
| `/T#h` | `TCh 10 div` | overall height |
| `/T#w` | `0` | overall width: 0 for auto (unscaled), >0 for absolute, <0 to scale (negated) |
| `/T#a` | `/C` | alignment: /C(entre) /L(eft) /R(ight) /J(ustify) /T(op) /B(ottom) /TJ /TL /TR /BL /BR (+ /JT etc.) |
| `/T#t` | `0` | tracking between characters or blocks (fraction of height, auto if width>0 & Justify) |
| `/T#b` | `false` | true to block-invert characters (cameo style) |
| `/T#m` | `0` | block monospace width (fraction of height or a character e.g. /M): 0 for no monospace |
| `/T#p` | `0.1` | block padding (fraction of height) |
| `/T#o` | `1` | block horizontal padding multiplier |
| `/T#r` | `0` | block corner radius (fraction of height): 0 for none, 1 for maximum rounding |
| `/T#g` | `0` | block gap for whitespace (fraction of height): 0 for auto (use advance width) |
| `/T#i` | `null` | italic angle (degrees anticlockwise): null for auto (font-embedded ItalicAngle) |
| `/T#-` | `false` | true for no `reversepath` of block charpath (TODO: needed for FontForge TT, why? ) |
| `/T#z` | `0` | z-index for layering |
| `/T#?` | `true` | true to show this custom text element |

(`#` is the text element number)

> ![Tip](assets/icons/tip-16.svg)\
> The height `/T#h` is the overall letter height.\
  The string width is squeezed or stretched to the overall width `/T#w`
  which if negative is scaled, e.g. `/T#w -1.2 arg` stretches to 120%,
  whereas positive is an absolute width and zero is the default string width.

</details>

## Resolution

> [!NOTE]
> Resolution, [aspect ratio](#aspect-ratio) and [scaling](#scaling) depend on factors too involved to delve into here – whether analogue/digital, PAL/NTSC/SECAM, line count, line time, sampling rate etc.
  but there are experts on the VideoHelp Forum[^14] and elsewhere with detailed answers.


In the vertical plane, analogue scan lines are inherently discrete.
In the horizontal the intensity is continuous but cannot alternate faster than the scan rate and video bandwidth allow under the sampling theorem[^15].
These constraints are specified by various standards, therefore analogue horizontal resolution can be approximated[^16].
The practical measure used is Television lines (TVL)[^17], explained in Alan Pemberton’s *Ponderings*[^18].

In simulating analogue test cards digitally, TCM simply scales the active analogue line time to the width `TCw` and the active scan lines to the height `TCh`.
This gives square unit pixels for 4:3 625-line replicas at the default 768x576 size
but applies scaling and warping for other values.

TCM takes no account of Kell factor[^19] and rounds pattern size up to even numbers
to simplify the maths and facilitate digital video post-processing.
So 625/50 has 575 active lines (25 frame blanking lines) but 576 is used (the default),
and 405/50 has 377 active lines (14 frame blanking lines) and height 378.
Units are arbitrary but PostScript/PDF points are 1/72" by default, or 1 pixel for [raster format](#user-content-raster-formats) images.


## Aspect ratio

TCM [size](#size) is detailed above; that defines the Storage Aspect Ratio (SAR) in pixels or points.

Changing the aspect ratio `TCr` expands or contracts the width accordingly
and the drawing algorithms compensate _without distorting element shapes_.
Element positions should therefore be anchored relative to centrelines or edges or other elements.

Widescreen aspects, being digital, retain 625-line [time-base](#user-content-time-based-scaling) scaling for frequency gratings, needle pulse widths and corner stripes,
which presumably lose their intended significance.

*Examples:* a 5:4 *GTP-A* and widescreen *BBC-D-improved* with altered text and square *BBC-F-electronic*

[![5:4 ratio](assets/ratio-54-thumb.png)](assets/ratio-54.png)
&nbsp;
[![widescreen ratio](assets/ratio-ws-thumb.png)](assets/ratio-ws.png)
&nbsp;
[![square ratio](assets/ratio-sq-thumb.png)](assets/ratio-sq.png)

## Scaling

Engineering documents specify the width of certain pattern elements in terms of [time](#user-content-time-based-scaling) (MHz or μs or lines).
TCM scales all other dimensions relative to the grid size to maintain [proportions](#user-content-proportional-scaling).

<details><summary>Scaling details</summary>
<a name='scaling-details'></a>


### Time-based scaling

TCM computes the width of frequency gratings, needle pulse lines and corner stripes in proportion to the 1μs width, where the total width corresponds to the active line time.
Values for these are found in BBC engineering documents.
The scaling operators for timed and periodic widths are `us` (microseconds) and `mhz` (megahertz), computed for the active line time.
The scaling operator for scan line heights is `lines`, computed for the active frame time.

*Example:* *BBC-C* centre frequency grating is 2MHz, so the stripe width is specified as\
`2 mhz div2` for the half period

*Example:* *BBC-C-625* needle pulse width is 0.2μs, specified as\
`/NPw 0.2 us arg`

*Example:* *BBC-F-electronic* grid width is 5 scan lines, specified as\
`/Glw 5 lines arg`

### Proportional scaling

The unit of scaling for all other graphic elements is the grid size, i.e. the length of one side of a graticule square.
This unit is named `/Gsz` and the main scaling [operator](#user-content-operators) for fixed elements is `xGsz`.

*Example:* *BBC-C* streak box outer width is 2.66 grid squares, specified as\
`/SBow 2.66 xGsz arg`

> ![Note](assets/icons/note-16.svg)\
> For *GTP-A*, which has no graticule, `Gsz` is the distance between adjacent horizontal castellation midpoints clamped within ±10% of the vertical ones.
  This makes elements shrink as the aspect ratio reduces, resulting in a 5:4 version close to the early TCA shown on Arthur Dungate’s 5x4 era page, see [test card links](#test-cards) and [ratio example](#aspect-ratio).

</details>

## Timing

TODO: note about 405/625 constants

TODO: note about rise/fall times In simulating analogue test cards digitally

## Colours

Colour can be expressed as
[greyscale](#user-content-greyscale),
[RGB](#user-content-rgb),
[YUV](#user-content-yuv),
[HSL](#user-content-hsl),
[HSB](#user-content-hsb) (HSV),
[unit interval](#user-content-unit-interval-colour-components) (UI)[^20]
or [named](#user-content-named-colours) colours.
There are special names for [chroma keying](#user-content-chroma-keying) and [random](#user-content-random-colour) colours.

<details><summary>Colour arguments</summary>
<a name='colour-arguments'></a>


### Greyscale

Grey shades are specified as a value from 0 to 255.

*Example:* `128` for mid-grey

> ![Tip](assets/icons/tip-16.svg)\
> Colour component values need not be integers, e.g. `127.5` is acceptable.

> ![Note](assets/icons/note-16.svg)\
> Regardless how a colour is specified,
  if it produces grey then the PostScript colour space is set to Gray,
  otherwise it is converted to RGB.\
  If colour is rendered to a grey/mono output device, e.g. `pnggray`, then GS emits a warning.

### RGB

RGB colours can be specified as an array of [Red Green Blue] values from 0 to 255:

*Example:* `[207 92 230]RGB` or just `[207 92 230]` (RGB is the default)

RGB can also be specified in hexadecimal #RRGGBB notation (case-insensitive) as a name or a string:

*Example:* `/#Cf5cE6` (name syntax), `(#Cf5cE6)` (string syntax)

### YUV

YUV was invented for colour television[^21] but the number of standards nowadays is bewildering.
The following are currently supported[^22]:

- `YUVDSD`: limited YCbCr &rarr; full RGB, ITU-R BT.601, for digital SDTV
- `YUVDHD`: limited YCbCr &rarr; full RGB, ITU-R BT.709, for digital HDTV
- `YUVFR`: full YCbCr &rarr; full RGB, with no footroom or headroom

*Example:* `[168 44 136]YUVDSD` or just `[168 44 136]YUV`

`YUV` defaults to `YUVDSD` about which Wikipedia has this to say:

> This form of Y′CbCr is used primarily for older standard-definition television systems,
  as it uses an RGB model that fits the phosphor emission characteristics of older CRTs[^23].

<!-- Math in collapsed section bug: avoid $G_y$, see https://github.com/orgs/community/discussions/57950 -->
To extend YUV conversions, add a matrix procedure like `YUVDSD` in [tcm-colour.ps](Resource/ProcSet/tcm-colour.ps)
to convert *Y* *C*<sub>b</sub> *C*<sub>r</sub> components to *R* *G* *B*
with constants *G*<sub>y</sub> *R*<sub>v</sub> *G*<sub>u</sub> *G*<sub>v</sub> *B*<sub>u</sub> *Y*<sub>o</sub> *C*<sub>o</sub>
for the matrix:

```math
\begin{bmatrix} R \\ G \\ B \end{bmatrix} =
\begin{bmatrix} G_y & 0 & R_v \\ G_y & G_u & G_v \\ G_y & B_u & 0 \end{bmatrix}
\times \begin{bmatrix} Y - Y_o \\ C_b - C_o \\ C_r - C_o \end{bmatrix}
```


### HSL

HSL colour is specified as an array of [Hue Saturation Lightness] values.\
Hue is an angle (0 to 360&deg;), and Saturation and Lightness are percentages (0 to 100%).

*Example:* `[310 60 90]HSL`

### HSB

HSB colour, a.k.a. HSV[^24], is specified as an array of [Hue Saturation Brightness] values.\
Hue is an angle (0 to 360&deg;), and Saturation and Brightness are percentages (0 to 100%).

*Example:* `[310 60 90]HSB`

`HSV` is an alias for `HSB`.


### Named colours

All the standardised X11 colour names[^25] are supported.
Colour names are case-insensitive and must not contain spaces.
Both `grey` and `gray` (US) are recognised.

*Example:* `/Lightgrey` (case-insensitive)


### Chroma keying

Colour names for chroma key compositing (case-insensitive) are:\
`/GreenScreen` (`[0 177 64]`)\
`/BlueScreen` (`[0 71 187]`)\
these seem most common but `[8 39 245]` is given as blue standard by Gerriets[^26].

Green screens are generally used now but blue screens were prominent in early television[^27].


### Random colour

Use `/RandomColour` or `/RandomGrey` (case-insensitive) for a randomly generated colour or greyscale value.

### Unit interval colour components

Whichever colour representation above is used, TCM has to convert all colour component values to the
unit interval[^20] (UI), i.e. real numbers between 0.0&nbsp;and&nbsp;1.0 incusive,
for PostScript to process.

Therefore TCM also accepts UI values for all colour components, with automatic UI detection.

*Example:* `0.75` (greyscale equivalent to `191`)

*Example:* `[0.812 0.361 0.902]RGB` (equivalent to `[207 92 230]RGB`)

*Example:* `[0.659 0.173 0.533]YUV` (equivalent to `[168 44 136]YUV`)

*Example:* `[0.806 0.6 0.9]HSB` (equivalent to `[290 60 90]HSB`)

> ![Note](assets/icons/note-16.svg)\
> UI detection interprets colour component value 1 as maximum,
  therefore it can be ambiguous when all component values are 1 or less.
  For instance greyscale `1` is white but `1.001` computes to almost black (1.001/255) because it is greater than 1.
  Similarly `[1 0 0]RGB` is red, not `#010000`, whereas `[1.001 0 0]` does compute close to `#010000`.
  However `[1 10 0]RGB`, `[100 0 1]YUV` and `[30 1 1]HSB` are not ambiguous because components lie outside the unit interval.
  To avoid ambiguity, add an epsilon to tip the relational test.


### Transparency

Unfilled areas are opaque or transparent depending on the [output format](#output-formats).

For transparent PNG, use `sDEVICE=png16malpha` or `sDEVICE=pngalpha`.
Transparent PDF is an outstanding task.

[Chroma keying](#user-content-chroma-keying) is a useful alternative to transparency for overlays.

### Gradients

TCM provides sinusoidal shading between two colours across a span where called for.
PS can paint any gradient, not necessarily continuous, by interpolation between samples or bounds.

</details>

<details><summary>Colour space</summary>
<a name='colour-space'></a>


TCM uses PS DeviceRGB and DeviceGray colour spaces which, by default, GS renders as sRGB and sRGB-linearised grey respectively.

Since GS release 9.0 the color architecture uses the ICC[^28] format for color management.
Specifically, for DeviceRGB and DeviceGray, the GS Color Management document[^29] states:

> “The profile default_gray.icc is defined to provide output along the neutral axis with an sRGB linearization.
   The profile default_rgb.icc is the V2 sRGB ICC profile”


</details>

## Fonts

How to
[list](#user-content-listing-fonts),
[add](#user-content-adding-fonts) and
[edit](#user-content-editing-fonts) fonts,
with notes about [![Block](assets/block.png)](#user-content-block-inverted-fonts) characters and historical [logo](#user-content-bbc-logo-fonts) fonts:

<details><summary>Font resources</summary>
<a name='font-resources'></a>


### Listing fonts

Use the [ps-fonts.ps](ps-fonts.ps) script to list fonts available to GhostScript,
including [added](#user-content-adding-fonts) fonts:

*Example*:\
`gs -q -IResource -sDEVICE=pdfwrite -o ps-fonts.pdf ps-fonts.ps`\
creates a PDF file `ps-fonts.pdf` listing the PostScript font names alphabetically with sample texts, like the sample below.
These are the PS `FontName` values to use for font arguments.\
![PS fonts](assets/ps-fonts.png)

### Adding fonts

TrueType and Type&nbsp;42 (encapsulated TrueType) fonts
can be added to the `Resource/Font` directory or to a dedicated directory – see [Finding files](finding-files) and [Environment variables](#user-content-environment-variables).
The filename must match the PS `FontName` in the file, which is often the filename minus extension and spaces.
If that fails, use a font inspector app:
- Mac: Font Book –> File –> Validate File…
- Linux: `fc-scan` dumps the `postscriptname`
- Windows: install [Font-Validator]

### Editing fonts

[FontForge] (open source) is good for creating, editing and converting fonts.
The *BBC-C* ident letter **C** is a Type&nbsp;42 font made with FontForge
because the font couldn’t be found (it’s close to a cropped circle).
The Replica icon ![](assets/icons/replica-16.svg) is also a single-glyph Type&nbsp;42 font, extracted from TTF.
And the GillSans-alt TTF is GillSans with altered weight for *GTP-A*, which also couldn’t be matched.

### Block-inverted fonts

Block-inverted fonts (a.k.a cameo) are hard to find
so TCM fashions them in PostScript by modifying the glyphs
(reversing paths and appending padded anticlockwise border).
Consequently, any font can be block-inverted.
The `ItalicAngle` embedded in the font determines the default slant
and characters can be monospaced with fixed width and tracking.
See [Text arguments](#user-content-text-arguments) for all block rendering argument details.

### BBC logo fonts

From inspection, websites reproducing early BBC logos are not very reliable.
The definitively font name according to
[Dave Jeffery’s blog](https://kecskebak.blogspot.com/2011/05/washington-post.html)
is Washington, from a BBC insider,
which he recreates in [FontForge] from BBC specimen sheets of the metal typeface –
perhaps like this similar
[Doric No. 1 Italic](https://archive.org/details/1959-stephenson-blake-printing-types/page/140/mode/2up?view=theater)
sheet from the Caslon Letter Foundry.
But vintage footage and photos reveal variants through the years –
differences in weight, number glyphs, gap between letter C pincers –
and did they use dry transfer lettering for the large physical cards?

Anyway, [Washington](https://code.google.com/archive/p/newoldtv/downloads) derives from
[Fette Kursiv Grotesk](https://fontsinuse.com/typefaces/100191/fette-kursiv-grotesk),
revised in 1950 as
[Old Gothic Bold Italic](https://fontsinuse.com/typefaces/31951/old-gothic-bold-italic),
itself digitised from 1962 drawings as
[Flight Center Gothic](https://hex.xyz/Flight_Center_Gothic/),
and another digital version of Fette Kursiv Grotesk is
[Derek AT Italic](https://fontsgeek.com/fonts/Derek-AT-Italic-Regular).

TCM block-inverts Derek AT Italic for *BBC-C-625* and *BBC-D*, and Washington Book for *BBC-F-optical*,
as they match closest in overlay tests.

Other fonts are easier to identify, e.g. Gill Sans, Helvetica.
Sanchez is used for the *BBC-F-electronic* ID.

</details>

## Command line interface

Run Ghostscript from the command line in a Linux/Mac Terminal or Windows Command Prompt.

> [!NOTE]
> The executable command is `gswin64c` on Windows and `gs` on most other platforms.
  Examples here use `gs` but Windows users should substitute `gswin64c`.

Further info: [GS User Guide: Invoking Ghostscript](https://ghostscript.readthedocs.io/en/latest/Use.html#invoking-ghostscript)

### Options

TCM only uses a few GS options:

<details><summary>Basic options</summary>
<a name='basic-options'></a>


- `-q` suppresses startup messages
- `-I` adds directories for file access
- `-o` sets the output filename and disables interactive mode
- `-r` sets the resolution (default 72 ppi)
- `-s` defines a name with a string value (without parenthesis)
- `-d` defines a name with a numeric or name value or `true`, `false`, `null`
- `-f` execute a file, used here for argument files
- `-+` execute a file and create an array of following arguments
- `--` end of options, execute following files

Further info: [GS User Guide: Command line options](https://ghostscript.readthedocs.io/en/latest/Use.html#command-line-options)

</details>

<details><summary>Environment variables</summary>
<a name='environment-variables'></a>


Use `GS_OPTIONS` to save CLI verbosity:

`export GS_OPTIONS='-q -IResource -dInterpolateControl=-1'`

or on Windows:

`set GS_OPTIONS="-q -IResource -dInterpolateControl=-1"`

`GS_FONTPATH` specifies font directories.

Further info: [GS User Guide: Summary of environment variables](https://ghostscript.readthedocs.io/en/latest/Use.html#summary-of-environment-variables)

</details>

<details><summary>Finding files</summary>
<a name='finding-files'></a>


By default Ghostscript runs with limited filesystem access (`SAFER` mode),
so directory access must be enabled explicitly:

The `Resource/` directory contains all TCM resources needed by `tcm.ps`

- `-IResource` allows access to files in the `Resource/` tree

For simplicity, put your images in `Resource/Image/` and your fonts in `Resource/Font/`
and use `-IResource` (see [Adding fonts](#user-content-adding-fonts)).

To use images in a subdirectory, say `MyPics`:

- `-IResource:MyPics` (on Windows use a semicolon, not a colon)

To use images in `$HOME/Pictures/TCMpics`, say:

- `-IResource:$HOME/Pictures/TCMpics`

And similarly for Windows:

- `-IResource;%HOMEDRIVE%%HOMEPATH%/Pictures/TCMpics` (use forward-slash /)

To use fonts in a subdirectory, say `MyFonts`:

- `-sFONTPATH=MyFonts`

Further info: [GS User Guide: How Ghostscript finds files](https://ghostscript.readthedocs.io/en/latest/Use.html#how-ghostscript-finds-files)

</details>

<details><summary>Rendering options</summary>
<a name='rendering-options'></a>


See also [colour space](#user-content-colour-space).

#### Interpolation

By default, GS renders images using nearest neighbour scaling.
To force images to be interpolated using bicubic scaling, use\
`-dInterpolateControl=-1` which is much slower.\
However GS can only interpolate non-skewed images at 0&deg; and 180&deg; rotation.

For PDF and EPS rendering there are Distiller parameters:\
`-dDownsampleXXXImages`\
`-dXXXImageDownsampleThreshold`\
`-dXXXImageDownsampleType`\
`-dXXXImageResolution`\
where `XXX` is `Color`, `Gray` or `Mono`.
Whether `-dInterpolateControl` takes precedence is not documented.

Further info:
[GS User Guide: -dInterpolateControl](https://ghostscript.readthedocs.io/en/latest/Use.html#dinterpolatecontrol-control-value),
[GS PDF/PS Devices: Distiller Parameters](https://ghostscript.readthedocs.io/en/latest/VectorDevices.html#distiller-parameters)

#### Antialiasing

For high quality image (not vector) rasterisations of text and graphics content, use subsample antialiasing:\
`-dTextAlphaBits=4 -dGraphicsAlphaBits=4` (set by default for `pngalpha` device).

For best PNG and TIFF rendering, use a high resolution with downscaling:\
`-r600 -dDownScaleFactor=2` gives an improved 300dpi image\
`-r1200 -dDownScaleFactor=6` gives 200dpi image\
this is the [recommended way](https://ghostscript.readthedocs.io/en/latest/Devices.html#png-file-format) to achieve antialiasing and gives better results than `-dTextAlphaBits=4 -dGraphicsAlphaBits=4` alone.

</details>

### Output formats

Use `-sDEVICE=` to select a driver for the output format.

See also [rendering options](#user-content-rendering-options) and [colour space](#user-content-colour-space) regarding rendering.

<details><summary>Vector formats</summary>
<a name='vector-formats'></a>


#### PDF

Use `sDEVICE=pdfwrite`.

#### EPS

Use `sDEVICE=eps2write`.\
Use option `-sEPSCrop` when converting from EPS to other formats with GS.

#### SVG

Not supported directly.

There are many PDF/EPS to SVG converters for download or online use.
I use [pdf2svg] from MacPorts, available as a Windows binary at [pdf2svg-windows],
which simply delegates to [Poppler] and [Cairo],\
preserving paths and even gradients without converting to bitmaps.
e.g. `pdf2svg myTC.pdf myTC.svg`

Further info: [GS User Guide: High level devices](https://ghostscript.readthedocs.io/en/latest/Devices.html#high-level-devices)

</details>

<details><summary>Raster formats</summary>
<a name='raster-formats'></a>


#### PNG

PNG is versatile and lossless, good for transparent areas, and is the recommended GS format for high-quality images.

PNG device summary
- `sDEVICE=png16malpha` (with `-dDownScaleFactor`) for 32-bit RGBA colour with transparency
- `sDEVICE=pngalpha` for 32-bit RGBA colour with transparency and default anti-aliasing
- `sDEVICE=png16m` for 24-bit RGB colour
- `sDEVICE=pnggray` for grayscale
- `sDEVICE=png256` for 8-bit indexed colour
- `sDEVICE=png16` for 4-bit indexed colour

Further info: [GS User Guide: PNG file format](https://ghostscript.readthedocs.io/en/latest/Devices.html#png-file-format)

#### TIFF, BMP, PNM, JPEG

The `tiffscaled` devices support the `DownScaleFactor` option:\
`gs -q -IResource -sDEVICE=tiffscaled24 -r576 -dDownScaleFactor=8 -sCompression=lzw -o tcf.tiff tcm.ps`

JPEG is not intended for graphics but `-dJPEGQ=100` maximises the quality.
Although undocumented, the `jpeg` device also supports `DownScaleFactor` but sets the DPI to the GS resolution, so\
`gs -IResource -sDEVICE=jpeg -dJPEGQ=100 -r576 -dDownScaleFactor=8 -o tcf576.jpg tcm.ps`\
for the default 576 pixel height makes a best-quality JPEG at 576 dpi downscaled from 6144x4608 internally (8x).
For normal display resolution, change the JFIF density metadata to 72, e.g. with [ExifTool] (open source):\
`exiftool -XResolution=72 -YResolution=72 -o tcf72.jpg tcf576.jpg`

See [GS User Guide: Image file formats](https://ghostscript.readthedocs.io/en/latest/Devices.html#image-file-formats)
for these and other raster formats Ghostscript can output directly.

#### WEBM, GIF

Not supported directly.

[ImageMagick] (open source) is good for CLI image conversions and manipulations,
and there are many graphics editing apps,
for instance [Affinity Photo] or [GIMP] (open source),\
e.g. `convert myTC.png myTC.webm` (ImageMagick) converts PNG to WEBM.

</details>

<details><summary>Video formats</summary>
<a name='video-formats'></a>


Video is not supported directly.

[FFmpeg] (open source) is a widely used CLI for making video files from raster images and other media sources, supporting many codecs and containers.
The following suggests some video and audio settings.

#### H.264/AAC (MP4)

Advanced Video Coding (AVC), see [H.264 Video Encoding Guide](https://trac.ffmpeg.org/wiki/Encode/H.264).

`-c:v libx264 -tune stillimage -pix_fmt yuv420p`\
`-c:a aac -ar 48000 -ac 2`

#### FFV1/PCM (MKV)

Lossless, see [FFV1 encoding cheatsheet](https://trac.ffmpeg.org/wiki/Encode/FFV1).

`-c:v ffv1 -level 3 -coder 1 -context 1 -g 1 -pix_fmt yuv420p`\
`-c:a pcm_s16le -ar 48000 -ac 2`

#### VP9/Opus (WEBM)

WebM 1280x720p@24,25,30, see [Recommended Settings for VP9](https://developers.google.com/media/vp9/settings/vod).

`-c:v libvpx-vp9 -b:v 1024k -minrate 512k -maxrate 1485k -crf 32 -quality good -g 240 -tile-columns 4 -threads 4 -pix_fmt yuv420p`\
`-c:a libopus`

#### Animated PNG

APNG muxer, see [apng](https://www.ffmpeg.org/ffmpeg-formats.html#toc-apng).
For much smaller files with 256 colours, include palette filters as for [GIF](#user-content-animated-gif).

`-f apng` specify format\
`-plays 0` loop forever\
`-final_delay n` delay n seconds between loops

Optimize with [Oxipng].

#### Animated GIF

For best results,` save or pipe concatenated uncompressed frames:

`-f yuv4mpegpipe`

and encode them with [gifski] (see [overlay example](#user-content-overlay-example)).

Otherwise, include these palette filters in the filtergraph,
see [`palettegen`](https://www.ffmpeg.org/ffmpeg-filters.html#palettegen) & [`paletteuse`](https://www.ffmpeg.org/ffmpeg-filters.html#paletteuse):

`[v]split[p][v]; [p]palettegen[p]; [v][p]paletteuse[v]`

Optimize with [Gifsicle].

</details>

## Video generation

> [!NOTE]
> These examples use the versatile [FFmpeg] CLI and [Bash] shell but can be adapted for Windows.

> [!TIP]
> Use ffmpeg options:\
  &bull; `-y` to overwrite output file\
  &bull; `-hide_banner` to suppress copyright and build infomation\
  &bull; `-v warning` to show warnings and errors only (hides banner too)\
  &bull; `-v error` to show errors only

### Static testcards

Here are some examples of making still videos of test card with or without sound:

<details><summary>Static examples</summary>
<a name='static-examples'></a>


First, make a test card image, say *BBC-F-electronic* (TCF, the default):\
`gs -q -IResource -sDEVICE=png16m -r576 -dDownScaleFactor=8 -o myTC.png tcm.ps`\
this makes a 24-bit sRGB antialiased PNG image, 768x576 pixels by default.

> ![Tip](assets/icons/tip-16.svg)\
> These examples make simple MP4 videos;
  see [Video formats](#user-content-video-formats) for other formats and better encoding options.

#### Silent test card

Create a 60 second 25 fps MP4 video from image without audio:\
`ffmpeg -i myTC.png -vf loop=-1:1 -pix_fmt yuv420p -t 60 myTC.mp4`\
(the [`loop`](https://www.ffmpeg.org/ffmpeg-filters.html#loop) filter here creates an infinite loop)

#### Test card with tone

Create a 60 second MP4 video from image with a 1kHz mono tone:\
`ffmpeg -i myTC.png -f lavfi -i sine=1000 -vf loop=-1:1 -pix_fmt yuv420p -t 60 myTC.mp4`\
(the [`sine`](https://www.ffmpeg.org/ffmpeg-filters.html#sine) audio source here creates a sine wave of 1000Hz)

#### Test card with music

Create a 1-hour MP4 video from image and looped audio:\
`ffmpeg -i myTC.png -stream_loop -1 -i myTC.wav -vf loop=-1:1 -pix_fmt yuv420p -t 1:0:0 myTC.mp4`

> ![Aside](assets/icons/aside-16.svg)\
> See the [Test Card Circle](#tv-community) link for historical test card and intermission background music lists.

</details>

### Overlays

Here is *BBC-D-improved* (1965 version) with transparent centre overlaying a video:

[![video example](assets/mrd-example-small.gif)](assets/mrd-example.gif)

<details><summary>Overlay example</summary>
<a name='overlay-example'></a>


#### Overlay commands

```bash
gs -IResource -sDEVICE=png16malpha -r1200 -dDownScaleFactor=4 -o tcD.png \
   -+ tcm.ps /TC /BBC-D-improved /CCf? false /SW? false /FB? false \
   /T-1s '(1965)' /T-2s '(The Magic Roundabout)'

ffmpeg -y -v warning -i magic.mkv -i tcD.png -filter_complex '
    [0]scale=-2:260, pad=768:576:-1:-1[tmr];
    [1]scale=768:576[tcd];
    [tmr][tcd]overlay[v]
    ' -map [v]:v -map 0:a -c:v libx264 -pix_fmt yuv420p -c:a aac magicD.mp4
```

The `gs` command `/CCf? /SW? /FB?` arguments switch off the centre circle fill, step wedge and frequency bars to make a transparent hole, and the `/T-1s /T-2s` arguments replace the caption text strings.
As [recommended](#user-content-antialiasing), `-r1200 -dDownScaleFactor=4` creates a high resolution antialiased PNG.

The `ffmpeg` command scales and centres the video 260px high (centre circle radius `CCr` x 2) and the PNG 576px high,
then overlays the two, producing a MP4 video complete with sound from the video.

The animated GIF above actually uses other [ffmpeg filters](https://www.ffmpeg.org/ffmpeg-filters.html#) too and a separate GIF encoder:

```bash
ffmpeg -y -v warning -ss 13:5.1 -t 5 -i magic.mkv -i tcD.png -filter_complex '
    [0]crop=1584:1056:170:12, zscale=ih*4/3:ih:f=spline36:r=full,
       monochrome, cas=0.75, normalize=smoothing=50, setsar=1/1, setdar=4/3,
       zscale=-2:260*504/768:f=spline36, pad=504:378:-1:-1[v];
    [1]zscale=504:378:f=spline36[i];
    [v][i]overlay, fps=15, format=yuv420p[g];
    ' -map [g]:v -f yuv4mpegpipe magicD.y4m
    gifski -q -o magicD.gif magicD.y4m
 # or -map [g]:v -f yuv4mpegpipe | gifski -q -o magicD.gif -
```

#### Overlay explanation

The `magic.mkv` source[^30] is a 1920x1080 60 fps progressive video with 3:2 aspect centred episodes.
A 5 second clip is extracted 13 minutes 5.1 seconds in.

Filters:

- [`crop`](https://www.ffmpeg.org/ffmpeg-filters.html#crop) cuts out the episodes
- crop rectangle obtained using [`cropdetect`](https://www.ffmpeg.org/ffmpeg-filters.html#cropdetect) on video source
- [`zscale`](https://www.ffmpeg.org/ffmpeg-filters.html#zscale) to `ih*4/3` width corrects the aspect from 3:2 to 4:3
  (you can use [`scale`](https://www.ffmpeg.org/ffmpeg-filters.html#scale) of course but [`zscale`](https://www.ffmpeg.org/ffmpeg-filters.html#zscale) passes color characteristics unchanged)
- the `spline36` scaling algorithm is good for downscaling sharp sources like testcards and animated content, as `lanczos` tends to introduce haloing/ringing artifacts
- [`monochrome`](https://www.ffmpeg.org/ffmpeg-filters.html#monochrome) converts video to grey (it looks grey but we don't know)
- [`cas`](https://www.ffmpeg.org/ffmpeg-filters.html#cas) sharpens video
- [`normalize`](https://www.ffmpeg.org/ffmpeg-filters.html#normalize) stretches dynamic range from black to white
- [`setsar`](https://www.ffmpeg.org/ffmpeg-filters.html#setsar) & [`setdar`](https://www.ffmpeg.org/ffmpeg-filters.html#setdar) (Sample/Pixel Aspect Ratio & Display Aspect Ratio) set square pixels and 4:3
- [`zscale`](https://www.ffmpeg.org/ffmpeg-filters.html#zscale) to `260*504/768` height reduces the video to double the centre circle radius `CCr` for the GIF width 504
- [`pad`](https://www.ffmpeg.org/ffmpeg-filters.html#pad) to `504:378` pads the video to the GIF size
- [`zscale`](https://www.ffmpeg.org/ffmpeg-filters.html#zscale) to `504:378` reduces the test card image source to the GIF size
- [`overlay`](https://www.ffmpeg.org/ffmpeg-filters.html#overlay) overlays the test card mask over the centred video
- [`fps`](https://www.ffmpeg.org/ffmpeg-filters.html#fps) sets the frame rate to 15 fps for the GIF
- [`format`](https://www.ffmpeg.org/ffmpeg-filters.html#format) converts to YUV for `yuv4mpegpipe`
- `-f yuv4mpegpipe` concatenates frames,
  saved as a [yuv4mpeg (.y4m)](https://linux.die.net/man/5/yuv4mpeg) file for [gifski] animation.


</details>

### DVDs

Making a DVD involves:

1. creating the needed media files to specification
1. building the directory structure
1. making an ISO image and burning it physical disk

<details><summary>DVD example</summary>
<a name='dvd-example'></a>


#### FreeCalRec601

Colour reproduction is a convoluted topic
but someone who understands is colour science guru and retro enthusiast Dan Mons.
His project [FreeCalRec601](https://github.com/danmons/FreeCalRec601)
is a Rec.601/BT.601[^31][^23] DVD and test pattern generator for calibrating Standard Definition (SD) CRT displays.
His [RetroRGB post](https://retrorgb.com/freecalrec601-dvds-for-calibrating-crts.html) about it has useful links and videos.

Like FreeCalRec601, TCM images have sRGB [colour space](#user-content-colour-space) when output by GS RGB devices,
so we just deploy the same [FFmpeg] options for SD DVD conformance.

> ![Aside](assets/icons/aside-16.svg)\
> FreeCalRec601 [build_images.sh](https://github.com/danmons/FreeCalRec601/blob/master/build_images.sh) makes sRGB colour chunks using [ImageMagick],
  for instance magenta75:\
  `convert -colorspace sRGB -type truecolor -depth 8 -size 180x144 xc:'rgb(218,98,218)' chunk_magenta75.tif`\
  the equivalent GS command being:\
  `gs -q -sDEVICE=tiff24nc -o chunk_magenta75.tif -dDEVICEWIDTHPOINTS=180 -dDEVICEHEIGHTPOINTS=144 -c '218 255 div 98 255 div 218 255 div setrgbcolor 0 0 180 144 rectfill showpage'`\
  and FreeCalRec601 ISOs built from GS-made sRGB colour chunks are empirically binary-identical to those built from ImageMagick chunks (tested for TIFF and PNG).


#### VOB commands

FreeCalRec601 [build_vob.sh](https://github.com/danmons/FreeCalRec601/blob/master/build_vob.sh) builds VOBs using [FFmpeg],
equivalent to this Bash snippet:

```bash
target=pal-dvd # or ntsc-dvd
vf=${target%-*}
if [[ $vf = pal ]]; then
    cs=bt601-6-625 cp=bt470bg ct=gamma28
else # ntsc
    cs=bt601-6-525 cp=smpte170m ct=smpte170m
fi

ffmpeg -y -v warning -loop 1 -i myTC.tif -i myTC.wav \
    -vf "
        colorspace=$cs:iall=bt709:range=tv:irange=tv,
        tinterlace=interleave_top:flags=low_pass_filter
    " \
    -target $target -flags +ildct+ilme \
    -color_primaries $cp -colorspace $cp -color_trc $ct -video_format $vf \
    -aspect 4:3 -shortest myTC-$vf.vob
```

This makes an anamorphic (720x576 4:3) interlaced DVD VOB in PAL or NTSC variant with audio.

#### VOB explanation

- `target`,`vf`,`cs`,`cp`,`ct` shell variables for PAL and NTSC variants
- `-loop` ([image2 demuxer](https://www.ffmpeg.org/ffmpeg-formats.html#image2-1)) loops the image frame
- `-vf` video filters:
  - [`colorspace`](https://www.ffmpeg.org/ffmpeg-filters.html#colorspace) converts the colour primaries, white point and gamma from bt709 (=sRGB) to bt601 for the target
  - [`tinterlace`](https://www.ffmpeg.org/ffmpeg-filters.html#tinterlace) makes the video interlaced, top field first, with vertical low-pass filtering (reduces interline twitter and Moiré artifacts)
- `-target` ([main options](https://www.ffmpeg.org/ffmpeg.html#Main-options)) sets video and audio format options for the target output, `pal-dvd` or `ntsc-dvd`
- `-flags` ([codec options](https://www.ffmpeg.org/ffmpeg-codecs.html#Codec-Options)) sets interlace encoding flags (cosine transform (DCT) and motion estimation)
- `-color_primaries`, `-colorspace`, `-color_trc` ([codec options](https://www.ffmpeg.org/ffmpeg-codecs.html#Codec-Options)) sets colour encoding values
- `-aspect` sets display aspect ratio (DAR)
- `-shortest` limits duration to the shortest input channel (audio here)

#### Authoring and burning

For free DVD authoring check out the [DVDAuthor] CLI and [DVDStyler] app.
[FreeCalRec601](https://github.com/danmons/FreeCalRec601) shows DVDAuthor in use with a menu.

To make an ISO image from the CLI:

Linux:\
`mkisofs -V 'Volume Name' -dvd-video -udf -J -o output.iso source-dir`

Mac:\
`hdiutil makehybrid -default-volume-name 'Volume Name' -udf -iso -joliet -o output.iso source-dir`

Windows:\
`Oscdimg.exe -l"Volume Name" -u1 -j1 source-dir output.iso`

Burning is usuallly a platform dependent proprietary command.

</details>

## Test card sources

Authentic originals of adequate quality and resolution are hard to find,
not least owing to the plethora of reconstructions that abound which on close scrutiny differ from reliable sources.
Of course there were no ‘masters’ as such in the early days,
and the cards, monoscopes and slides all differed slightly.

### Originals

- [BBC Testcards](https://tvark.org/features/testcards/bbc-testcards)
  – lots of authentic captures at the online TV museum [TVARK](https://tvark.org/), many dated
- [Transdiffusion article on Test Card C](https://transdiffusion.org/2017/04/17/the-tuning-signal-test-card-c-and-tracing-faults/)
  – early version of BBC pattern C with fault-tracing guidance,
    reproduced from *A Beginner’s Guide to Television* by F.J. Camm, 1958
- [Information Sheet 2021A](http://tech-ops.co.uk/next/2012/08/test-cards/)
  – BBC patterns C, D, E dated 1964 (it is not clear whether all images are from the same Info Sheet)
- [BBC Monograph 69 by George Hersee](https://downloads.bbc.co.uk/rd/pubs/archive/pdffiles/monographs/bbc_monograph_69.pdf)
  – BBC patterns A, C, D, F, dated 1967
- [BBC C (625)](https://tvark.org/media/1998i/2020-05-15/a4caf939a8d9a72a7882e4d2f2fd5ca26054bc19.jpg)
  – BBC 625-line pattern C (E replacement) from the [TVARK](https://tvark.org/features/testcards/bbc-testcards)
- [Test Card D (improved)](https://64.media.tumblr.com/a09924868d6901752c973f789a0d96d3/tumblr_noe40mZPWc1uvcudho1_1280.jpg)
  – BBC pattern D 1965 version from Transdiffusion (unfound link)
- [Test Card F (original)](https://i7.photobucket.com/albums/y276/pleccy2000/TCF-Original.jpg)
  – early BBC pattern F from the [TV Forum (archive)](https://www.tvforum.co.uk/tvhome/50-years-test-card-f-42738)
- [Information Sheet 4306(6)](https://www.bbceng.info/additions/2020/Eng-inf/Eng%20Inf%20Dept%20Sheet%204306(6)%20Test%20Cards%20F%20&%20G%20(full%20quality).pdf)
  – contains BBC pattern F, dated 1967
- [Test Card F (optical vs electronic)](https://archive.ph/VpVwc)
  – slide scan from the archived barney-wol site [Peter Vince (G8ZZR)]
  with excellent discussion on optical and digital features
  (see also [Eng Inf No.10 p.8](https://www.bbceng.info/Eng_Inf/eng-inf-files/EngInf10.pdf#page=8)
   and [Eng Inf No.18 p.9](https://www.bbceng.info/Eng_Inf/eng-inf-files/EngInf18.pdf#page=9))
- [Test Card F remembered](https://www.thesun.ie/tv/8237463/remember-tes-card-girl-tv-carole-hersee-unrecognisable/)
  – BBC electronic pattern F in [high resolution](https://www.thesun.co.uk/wp-content/uploads/2016/08/nintchdbpict000000243337.jpg) as confirmed by its [subtle errors](https://archive.ph/VpVwc)
- [Test Card J](https://archive.ph/RhAE8)
  – from the archived barney-wol site,
  this shows [EBU R 103](https://tech.ebu.ch/files/live/sites/tech/files/shared/r/r103.pdf#page=5)
  ‘broadcast-safe’ 8-bit colour values 16-253 (except side magentas, possibly in error)
- [Test Card J Carole Hersee](https://www.flickr.com/photos/bbccouk/3113496392/sizes/c/)
  – high resolution from the [Flickr bbccouk photostream](https://www.flickr.com/photos/bbccouk/)

### Reconstructions

- [The Rewind Team](https://rewind.thetvroom.com/38764/features/the-history-of-the-bbc-trade-test-transmission-part-1-4/)
  – montages of mixed originals and reconstructions with useful commentary
- [The Test Card Circle](https://www.testcardcircle.org.uk/tchistory.html)
  – most of the images shown are reconstructions
- [sub-TV ATV Test Cards](http://sub-tv.co.uk/atvtestcards.asp) and
  [625 TV Room](https://625.uk.com/tv_logos/flash2.htm#testcards)
  – many thumbnail re-creations by artist Dave Jeffery
- [DeviantArt LDD101](https://www.deviantart.com/ldd101/gallery)
  – lots of patterns from a Vietnam artist
- all manor of commercial outlets like Alamy, Adobe Stock etc. sell test cards of dubious authenticity

In general, any analogue-era test pattern with uniform grey background or perfect typography or no telltale signs of handcrafted workmanship is likely to be a reconstruction.

## Graphical user interface

There isn’t one but TCM lends itself to be GUI-driven easily.

### FML Test Card Maker

A neat freeware GUI test card maker for Windows exists called CardMaker by FML.
Although old and unmaintained it still works well.
Indeed it is so useful that it deserves a mention here:

<details><summary>CardMaker</summary>
<a name='cardmaker'></a>


<a href='assets/cm/CardMaker.png'><img src='assets/cm/CardMaker-thumb.png' alt='FML CardMaker' align='right'></a>

Funsville Memetic Laboratories (FML) is the web space of Steve Heap, a.k.a. [FMLTheGeneral](https://www.youtube.com/@FMLTheGeneral/videos), author of CardMaker on the defunct oodletuz\.fsnet\.co\.uk domain but available on The Wayback Machine. Pertinent links are:

- [FML Test Card Maker](https://web.archive.org/web/20151010221017/http://www.oodletuz.fsnet.co.uk/soft/tcmaker.htm) – the `tcmaker.zip` file contains the `CardMaker.exe` executable, Compiled HTML Help (CHM), resource files, instructions and sample Test Card Definition (TCD) files
- [The TCD Resource](https://web.archive.org/web/20160305053742/http://www.oodletuz.fsnet.co.uk/tcd/index.htm) – a lot of TCD files for UK, European and other world standard test cards
- [Testcards by Wenlock Burton (VK3YWB)](https://www.flickr.com/photos/wenlockburton/albums/72157629092497514/with/2884520670) – a Flickr album of 80 more test card reconstructions using CardMaker
- [Wenlock’s Testcard Galleries and TCDs](https://www.oocities.org/wenlockburton/testcards/index.htm) – showcase and a downloadable zip file of all his TCDs on the oocities\.org archive.

TCD files are conceptually like TCM templates: they define pattern objects and layer properties.
The TCD format is plain text: tab- and space-separated property values
stored as implicit fixed-point integers (2 dp), integer 24-bit RGB colours, and text.

The image (click to enlarge) shows CardMaker running on Windows 10
with two layers: pattern elements on the left and cutouts on the right,
also a CHM Help window and a Paint window of the image generated from the PM5544 TCD sample.

CardMaker generates lossless BMP and variable-quality JPEG images only, no vector formats.
Despite its legacy 32-bit 2004 vintage it is well designed, intuitive and functional.
For detailed information see the [CardMaker Help](assets/cm/CardMaker-help.pdf) PDF converted from the CHM.

</details>

## In memoriam

### Gordon J. King&#x2020;

This project is dedicated to Gordon J. King (G4VFV) whose lucid servicing handbooks
helped nurture my teenage passion for practical electronics
which led to an enjoyable and fulfilling career, including a training spell with the BBC.
Back then, after persistently borrowing GJK’s books from the Horsham lending library,
I managed to save enough money to buy my own (below).
Even now they are a fascinating read, and many principles explained are relevant today.

![Radio and Audio Servicing Handbook](assets/Radio-and-Audio-Servicing-Handbook-ed2-thumb.png) &nbsp;
![Television Servicing Handbook](assets/Television-Servicing-Handbook-ed2-thumb.png) &nbsp;
![Colour Television Servicing](assets/Colour-Television-Servicing-ed3-thumb.png) &nbsp;


This year (2025) I became aware that I had been living two streets away from Mr&nbsp;King
in Furzeham, Brixham, for 14 years until he died in 2010.
That August, soon after his funeral service, I began as organist at the same [church](https://youtu.be/OmLH3yhwXrQ), still unaware.
Anyway, he mentored through his writings, covering the heyday of analogue electronics
and milestone transitions from valve to semiconductor, monochrome to colour, analogue to digital…
RIP GJK.

### Tributes

- [Torbay Weekly: article](https://www.torbayweekly.co.uk/news/home/1253834/a-remarkable-engineer-in-danger-of-being-lost-in-history.html)
  – the story of Gordon King by Ian Handford, 2023
- [SuperannRTÉ.ie: obituary & tributes](https://superannrte.ie/index.php?option=com_content&view=article&id=851:death-of-gordon-j-king-author-and-editor-practical-wireless-851&catid=10&Itemid=115)
  – Gordon J King, Author and Editor Practical Wireless
- [UK Vintage Radio forum](https://www.vintage-radio.net/forum/showthread.php?t=54437)
  – discussion thread on Gordon J. King (3 pages)
- [Bibliography](https://www.vintage-radio.net/forum/showthread.php?t=140536)
  – informal list of GJK book titles compiled by [Andrewausfa](https://www.youtube.com/@Andrewausfa)

## Further reading

### Television history

- [BBC Television from Alexandra Palace, 1952–63](http://www.bbctv-ap.co.uk/bbctvp1.htm) – personal experiences by Arthur Dungate, with [index](http://www.bbctv-ap.co.uk/a-zindx.htm)
- [A Tech Ops History](http://www.tech-ops.co.uk/) – in stories and pictures, by Bernie Newnham
- [British Heritage Television](https://405-line.tv/) – 405-line demo transmissions and [A Brief History](https://405-line.tv/tv-history/)
- [List of years in British television](https://en.wikipedia.org/wiki/List_of_years_in_British_television) – Wikipedia
- [The Story of BBC Television Idents](https://www.bbc.com/historyofthebbc/research/bbc-idents) – the BBC’s on-air look from 1936 to the present day
- [World Radio History](https://www.worldradiohistory.com/Home-UK.htm) – UK collection of documents and publications
- [The Transdiffusion Broadcasting System](https://transdiffusion.org/) – a broadcasting archive for research and education
- [TVARK](https://tvark.org/) – a comprehensive TV archive of Betamax and VHS home recordings
- [TV Camera Museum](https://tvcameramuseum.org/) – virtual camera museum with interesting [monoscope](https://tvcameramuseum.org/marconi/bd665/p-1.html) test card grabs
- [Early Television Foundation](https://earlytelevision.org/) – interesting American site with a [British and European](https://earlytelevision.org/postwar_british.html) section

### Technical

- [BBCeng.info](https://www.bbceng.info/Information/eng_inf_top.htm) – BBC Engineering Information from 1922 to 1997
- [BBC Engineering Monographs](https://www.bbc.co.uk/rd/publications/engineering-monographs) – 115 downloadable editions from 1955 to 1980
- [BBC Technical Instruction: Test Waveforms](https://www.bbceng.info/ti/non-eqpt/TI_P2_Part3_Test%20Waveforms.pdf) – 405-line waveforms (p.11) and 625 (p.17)
- [A Broader Aspect](https://transdiffusion.org/2006/03/31/broader_aspect/) – Transdiffusion article on early television aspect ratios
- [EBU Technical Recommendation R92-1999](https://tech.ebu.ch/docs/r/r092.pdf) – active picture area and centring in analogue and digital 625/50 television systems
- [Analog television](https://en.wikipedia.org/wiki/Analog_television) – Wikipedia
- [Television Technical Theory: Unplugged](https://danalee.ca/ttt/) & [Analog Video](https://danalee.ca/ttt/analog_video.htm) – comprehensive insights by Dana M. Lee
- [List of common display resolutions: Analog systems](https://en.wikipedia.org/wiki/List_of_common_display_resolutions#Analog_systems) – approximate dots x lines resolution
- [World Analogue Television Standards and Waveforms](https://www.bbceng.info/Technical%20Reviews/World%20Analogue%20Television%20Standards%20and%20Waveforms.pdf) – summary of colour standards at the time they were current
- [PAL encoding](https://en.wikipedia.org/wiki/PAL) – Wikipedia
- [Limiting of YUV Digital Video Signals](https://downloads.bbc.co.uk/rd/pubs/reports/1987-22.pdf) – a BBC Research Report
- [YUV Color Calculator](https://res18h39.netlify.app/color) – colour conversion calculator
- [BBC HD test signals](https://www.bbc.co.uk/blogs/bbcinternet/2008/12/a_christmas_present_from_the_h.html) – Andy Quested, BBC Internet Blog

### Test cards

- [5x4 era](http://www.bbctv-ap.co.uk/gallery1.htm) and [early 4x3 cards](http://www.bbctv-ap.co.uk/gallery2.htm) – by Arthur Dungate
- [Test Card History](https://web.archive.org/web/20160304132214/http://www.pembers.freeserve.co.uk/Test-Cards/index.html) – excellent background by Alan Pemberton
- [TVARK: BBC Testcards](https://tvark.org/features/testcards/bbc-testcards) – archive of test card video recordings
- [The Test Card Girl](https://youtu.be/t7yIXLx5on0) – AMTV documentary video: The Lasting Legacy of Test Card F
- [Technical descriptions of UK test cards](https://web.archive.org/web/20160409090425/http://www.pembers.freeserve.co.uk/Test-Cards/Test-Card-Technical.html) – authoritative information by Alan Pemberton
- [Tim Worthington: The Test Card](https://timworthington.blogspot.com/2013/11/the-fifty-fourth-annual-academy-salute.html) – a humorous take
- see also [Test card sources](#test-card-sources) links above

### Other test card projects

- repo [danmons/FreeCalRec601](https://github.com/danmons/FreeCalRec601) – accurate Rec.601 SD calibration DVD and test pattern generator
- repo [davecrump/vidsource](https://github.com/davecrump/vidsource) – [BATC](https://batc.org.uk/) Composite Video Source for [Raspberry Pi Zero](https://www.raspberrypi.com/products/raspberry-pi-zero/)
- repo [sarodp/myatv](https://github.com/sarodp/myatv) – amateur TV test pattern generator from static JPEG images for Raspberry Pi
- repo [georgik/esp32-monoscope-pattern](https://github.com/georgik/esp32-monoscope-pattern) – for [ESP32](https://www.espressif.com/en/products/socs/esp32), simulates classic test patterns with old TV effects
- repo [edent/SVGtestcard](https://github.com/edent/SVGtestcard) – SVG 1080p test Card based on BBC HD pattern
- repo [jyun9504/tv-test-card](https://github.com/jyun9504/tv-test-card) – a widescreen Vue implementation
- repo [lordxeorus/Test-Patterns](https://github.com/lordxeorus/Test-Patterns) – FFMpeg colour bars generation: EBU 100/75% for PAL and SMPTE for NTSC
- [TV Testcard Generator](https://testcardgen.onrender.com/) – interactive online tool for quick TC generation on the [Render](https://render.com/) platform
- [FML Test Card Maker](https://web.archive.org/web/20151010221017/http://www.oodletuz.fsnet.co.uk/soft/tcmaker.htm) – Windows tool, creates test cards and patterns from elements, see [CardMaker](#user-content-cardmaker)

### TV Community

- [British Amateur Television Club](https://batc.org.uk/) – promotes all aspects of television past and present
- [British Vintage Wireless Society](https://www.bvws.org.uk/) – preservation of vintage radio and related equipment, history, technical data
- [UK Vintage Radio Repair and Restoration](https://www.vintage-radio.net/) – discussion forum
- [Radios-TV](https://www.radios-tv.co.uk/) – Vintage radio & television blog and forum
- [TV Forum](https://www.tvforum.co.uk/) – discussion forum, static archive since 2021
- [Golborne Vintage Radio](https://www.golbornevintageradio.co.uk/) – forums on everything vintage
- [The Test Card Circle](https://www.testcardcircle.org.uk/) – for test card music enthusiasts

### PostScript links

- [PostScript Language Reference Manual](https://www.adobe.com/jp/print/postscript/pdfs/PLRM.pdf) – Adobe Systems PLRM LanguageLevel 3
- [ttf2pscid2](https://github.com/scriptituk/ttf2pscid2) – TTF to PostScript Type 2 CIDFont Converter by [scriptituk]
- [Lettering Designer](https://www.tribalsigns.co.uk/shop/custom-lettering/72-custom-lettering.html) – PostScript generated signage developed by [scriptituk]

### Useful tools

- [Affinity Photo] – low cost professional photo editing app
- [Cairo] – 2D graphics library
- [DVDAuthor] – for authoring DVD file and directory structure
- [DVDStyler] – cross-platform free DVD authoring, front end for [DVDAuthor]
- [ExifTool] – for manipulating metadata in a wide variety of file types
- [FFmpeg] – software suite that handles multimedia data
- [FontForge] – comprehensive font editor
- [Font-Validator] – initially developed by Microsoft, has cross-platform binary downloads
- [Gifsicle] – GIF editor and optimiser
- [Gifski] – high-quality GIF animation encoder using [pngquant]
- [GIMP] – GNU Image Manipulation Program
- [ImageMagick] – for editing and manipulating digital images
- [Oxipng] – PNG/APNG compression optimizer
- [pdf2svg] – simple PDF to SVG converter using [Poppler] and [Cairo]
- [pdf2svg-windows] – ditto for Windows
- [Poppler] – PDF rendering library
- [pngquant] – lossy compression of PNG images
- [xfade-easing] – video transition effects for FFmpeg Xfade filter by [scriptituk]

Primary: `#007bff` (Blue)

### Footnotes

<!-- Link references -->

[Affinity Photo]: https://www.affinity.studio/photo-editing-software
[Bash]: https://www.gnu.org/software/bash/
[Cairo]: https://cairographics.org/
[DVDAuthor]: https://dvdauthor.sourceforge.net/
[DVDStyler]: https://www.dvdstyler.org/
[ExifTool]: https://exiftool.org/
[FFmpeg]: https://www.ffmpeg.org/
[FontForge]: https://fontforge.org/
[Font-Validator]: https://github.com/HinTak/Font-Validator
[Gifsicle]: https://www.lcdf.org/gifsicle/
[Gifski]: https://gif.ski/
[GIMP]: https://www.gimp.org/
[ImageMagick]: https://imagemagick.org/
[Oxipng]: https://github.com/oxipng/oxipng
[pdf2svg]: https://github.com/dawbarton/pdf2svg
[pdf2svg-windows]: https://github.com/jalios/pdf2svg-windows
[Poppler]: https://poppler.freedesktop.org/
[pngquant]: https://pngquant.org/
[xfade-easing]: https://github.com/scriptituk/xfade-easing

[scriptituk]: https://github.com/scriptituk
[^1]: [The PostScript Language: A Comprehensive Guide](https://smallusefultips.com/what-is-postscript-language/) – by SmallUsefulTips

[^2]: [Page Description Language](https://en.wikipedia.org/wiki/Page_description_language) – Wikipedia

[^3]: [The history of PostScript](https://www.prepressure.com/postscript/basics/history) – by Laurens Leurs

[^4]: [Anastigmatix Import](https://www.anastigmatix.net/postscript/Import.html) – PostScript resource for embedding media file elements

[^5]: [Object-oriented programming](https://en.wikipedia.org/wiki/Object-oriented_programming) – Wikipedia

[^6]: [Encapsulated PostScript](https://en.wikipedia.org/wiki/Encapsulated_PostScript) – Wikipedia

[^7]: [Forth programming language](https://en.wikipedia.org/wiki/Forth_(programming_language)) – Wikipedia

[^8]: [Philips circle pattern](https://en.wikipedia.org/wiki/Philips_circle_pattern) – Wikipedia

[^9]: [CSS z-index property](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index) – Mozilla MDN Web Docs

[^10]: [Unit square](https://en.wikipedia.org/wiki/Unit_square) – Wikipedia

[^11]: [Reuleaux polygon](https://en.wikipedia.org/wiki/Reuleaux_polygon) – Wikipedia

[^12]: [Scalar projection](https://en.wikipedia.org/wiki/Scalar_projection) – Wikipedia

[^13]: [Document Structuring Conventions](https://en.wikipedia.org/wiki/Document_Structuring_Conventions) – Wikipedia

[^14] [VideoHelp Forum](https://forum.videohelp.com/) – huge video knowledgebase since 1999

[^15]: [Sampling theorem](https://en.wikipedia.org/wiki/Nyquist–Shannon_sampling_theorem) – Wikipedia

[^16]: [List of common display resolutions](https://en.wikipedia.org/wiki/List_of_common_display_resolutions#Analog_systems) – Wikipedia

[^17]: [Television lines (TVL)](https://en.wikipedia.org/wiki/Television_lines) – Wikipedia

[^18]: [Technical descriptions of UK test cards: Resolution](https://web.archive.org/web/20160409090425/http://www.pembers.freeserve.co.uk/Test-Cards/Test-Card-Technical.html#Resolution) – Alan Pemberton

[^19]: [Kell factor](https://en.wikipedia.org/wiki/Kell_factor) – Wikipedia

[^20]: [Unit interval](https://en.wikipedia.org/wiki/Unit_interval) – Wikipedia

[^21]: [Y′UV History](https://en.wikipedia.org/wiki/Y′UV#History) – Wikipedia

[^22]: [YUV – RGB Conversion](https://archive.ph/okUB) – archived from equasys GmbH

[^23]: [ITU-R BT.601 conversion](https://en.wikipedia.org/wiki/YCbCr#ITU-R_BT.601_conversion) – Wikipedia

[^24]: [HSL and HSV](https://en.wikipedia.org/wiki/HSL_and_HSV) – Wikipedia

[^25]: [X11 colour names](https://en.wikipedia.org/wiki/X11_color_names#Color_name_chart) – Wikipedia

[^26]: [Green screen / blue screen technique —> Color location](https://www.gerriets.com/gb/page/tv-and-studio-supplies/) – by PremiumBeat (Shutterstock)

[^27]: [Blue Screen vs Green Screen](https://www.premiumbeat.com/blog/blue-screen-vs-green-screen/) – Gerriets, specialist for stage and event equipment

[^28]: [International Color Consortium](https://www.color.org/) – ICC specification

[^29]: [Ghostscript 9 Color Management](https://ghostscript.com/docs/GS9_Color_Management.pdf) – color architecture in Ghostscript Release 9

[^30]: [The Magic Roundabout Series 1 1965–68 (incomplete)](https://youtu.be/jS2IlF9GEco) – 5 episodes, not 224, because of lost media

[^31]: [Rec.601/BT.601](https://en.wikipedia.org/wiki/Rec._601) – Wikipedia, ‘the bridge that joined the analogue and digital worlds’

