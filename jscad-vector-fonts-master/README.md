# Vectors fonts and serializer for the @jscad projet

## Using vector fonts as jscad module

1. Download one or more fonts from the [fonts/vector](fonts/vector) directory.
2. Include the font file in your project like any other module.
3. To access the font object simply add the `Font` suffix to the font name.

```javascript
// Include the font file in your project like any other module.
include('fonts/camBamStick1.js');

function main (params) {
  let height = 20;             // text height (xHeight)
  let extrudeOffset = 2;       // extrusion offset
  let font = camBamStick1Font; // font object (! NOTE the "Font" suffix)
  let text = vectorText({ font, height, extrudeOffset }, 'OpenJSCAD');

  return csgFromSegments(extrudeOffset, text);
}

function csgFromSegments (extrudeOffset, segments) {
  let output = [];
  for (let i = 0, il = segments.length; i < il; i++) {
    output.push(rectangular_extrude(segments[i], { w: extrudeOffset, h: 2 }));
  }
  return union(output);
}
```

## Using vector fonts as node module

```javascript
const myFont = require('fonts/camBamStick1');
const myText = vectorText({ font: myFont }, 'OpenJSCAD');
```

## Serialize vector fonts

A serializer is provided in this repository, which allows you to serialize your own fonts. You will have to find fonts called single-line, if you do not know what it is I refer you to [this page](http://imajeenyus.com/computer/20150110_single_line_fonts/index.shtml) (most of the fonts proposed here come from there).

### Installation
```
npm install
```

### Usages

```
npm run serialize [-- params]
```
By default, the script serializes all the fonts found in the `./fonts/opentype directory` to the `./fonts/vector directory`.
Type `npm run serialize -- -h` for more options...

```
 Usage: serializer [options] [inputPath] [outputPath]

  Options:

    -i, --input-path   <path>  path to a directory containing some Opentype font files
    -o, --output-path  <path>  path to a directory where the vector fonts will be saved
    -s, --font-size    <int>   font size in pixels; default = 500
    -d, --decimals     <int>   font decimals precision; default = 0
    -r, --replace              replace files that already exist in the output path
    -v, --version              output the version number
    -h, --help                 output usage information
```
