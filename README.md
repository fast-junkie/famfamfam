So... these are the unsung famfamfam icons as CSS, unsung meaning _"so widely used and yet so under appreciated"_, not the actually images themselves but the base64 data representation of said images. All rolled up into three CSS files.

```
dist/fj.famfamfam-min.css
- Includes all silk icons and flags.

dist/fj.famfamfam-silk-min.css
- Includes the silk icons only.

dist/fj.famfamfam-flag-min.css
- Includes the flag icons only.
```

Usage is totally based on my needs... sorry folks, sorta.  
Class names are the icon image names, if the icon name contained an `_` it was replaced
with a `-` with an `fj-` prefix.
```css
/*
 * To get the base icon or flag
*/
<span class="fj fj-webcam"></span>

/* 
 * For a and span tags I also added a way to 
 * position the image with a text item.
 */
<a href="http://famfamfam.com/" class="fj fj-bg-start fj-webcam">famfamfam.com</a>
<a href="http://famfamfam.com/" class="fj fj-bg-end fj-webcam">famfamfam.com</a>
```


# tl;dr

## Overview

In a nutshell, my icon strategy was totally shanghai'd from [Bootstrap's Icons](https://icons.getbootstrap.com/).

BUT... instead of fonts... I am using the famfamfam silk icon and flag png's in `base64` data format as a CSS `background-image` URL _(that's a mouthful)_.

---
- [famfamfam.com](http://www.famfamfam.com/) - _(was... or seemed... no longer in holders control)_  
  - [famfamfam.com](https://web.archive.org/web/20230109095739/http://www.famfamfam.com/) - _(internet archive alternate)_
---

## Details

Note the included `archive` directory contains the last known zip files I had in my possession, added for posterity.

SO... first I ripped the `exif` data from each image using ExifTool.

```
ExifTool is a platform-independent Perl library plus a command-line application for reading, writing and editing meta information in a wide variety of files.
                                        ~ Phil Harvey (exiftool.org)
```
And yes...! I did use the verboten `-all=` flag, see the below example.

Example:
```
-- Original Image OUT:

ExifTool Version Number         : 12.40
File Name                       : webcam.png_original
Directory                       : .
File Size                       : 728 bytes
File Modification Date/Time     : 2023:01:18 06:40:56-05:00
File Access Date/Time           : 2023:01:18 06:44:31-05:00
File Inode Change Date/Time     : 2023:01:18 06:43:32-05:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 16
Image Height                    : 16
Bit Depth                       : 8
Color Type                      : RGB with Alpha
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Gamma                           : 2.2222
Software                        : Adobe ImageReady
Image Size                      : 16x16
Megapixels                      : 0.000256

-- After Rip OUT:

ExifTool Version Number         : 12.40
File Name                       : webcam.png
Directory                       : .
File Size                       : 675 bytes
File Modification Date/Time     : 2023:01:18 06:43:32-05:00
File Access Date/Time           : 2023:01:18 06:43:35-05:00
File Inode Change Date/Time     : 2023:01:18 06:43:32-05:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 16
Image Height                    : 16
Bit Depth                       : 8
Color Type                      : RGB with Alpha
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Image Size                      : 16x16
Megapixels                      : 0.000256
```

As you can see... not a lot of loss regarding the image quality.

Moving on...

`base64`, I ran each newly `exif` stripped image against `base64 -w 0 <icon.png>`. Then jammed everything into a JSON array which I used to produce the output in a CSS template.

All via a `node.js` script running `fs, fs/promises, util[promisify], child_process[exec]`. Nothing to write home about... just a lazy mans way of parsing 1200+ png files and getting them out to a usable CSS file.

Sorry, but that code will not be available as developers get so janky when looking at code not their own _(and there were no tests... some nested promises... wha wha wha trust me I circumvented some serious drama here)_.

No fancy build process... just some vanilla `npm`.

```javascript
npm run build // it'll get you there...
```

## Why
Good damn question...