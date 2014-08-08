CSS3MultiColumn
===============

An update to CSS3MultiColumn by Cédric Savarese to support HTML5 elements.

The original code can be found here:
http://www.csscripting.com/css-multi-column/


### Initializing

##### With Modernizr (recommended)

*Keep your js payload lean by only loading this library if it's actually required:*

[Download a build of modernizr that includes the CSS Columns check](http://modernizr.com/download/#-csscolumns-touch-shiv-cssclasses-teststyles-testprop-testallprops-prefixes-domprefixes-load)

Put `css3-multi-column.min.js` in your project's javascripts folder.

Load your Modernizr build and application js after your stylesheets.

> Do **not** load `css3-multi-column.min.js` here! (it will get pulled in by Modernizr later.)

```html
<link rel="stylesheet" type="text/css" href="stylesheet.css" />
<script type="text/javascript" src="modernizr.custom.js"></script>
<script type="text/javascript" src="all.js"></script>
```

Add this to your javascript file (after modernizr has loaded):

```javascript
Modernizr.load({
  test : Modernizr.csscolumns,
  nope : 'css3-multi-column.min.js',
});
```

This will load the CSSColumns polyfill *only* when Modernizr detects a browser without native CSS Columns support.

##### Without Modernizr

Upload the script to your site.
Attach the script after the links to your stylesheet(s). Example:
```
<link rel="stylesheet" type="text/css" href="stylesheet.css" />
<script type="text/javascript" src="css3-multi-column.js"></script>
```

### Usage

You can now use any of these CSS3 multi-column properties in your stylesheet (providing that you understand the limitations given below).

New CSS Property | Type                | Example
-----------------|---------------------|----------------
column-count     | a number            | 3
column-width     | a value in pixels   | 200px
column-gap 	     | a value in pixels   | 10px
column-rule      | a border definition | 1px solid #000

Limitations (as of version 1.0beta)

Values for column-width and column-gap must be given in pixels. You must include column-count and use long-hand syntax.
The implementation relies on a light javascript css parsers. Avoid complex css structures (like cascading rules).

This is ok:

    .article {
       column-count: 3;
       column-gap: 20px;
    }

This is likely to break:

    #somearticleid {
        column-count: 3;
    }
    .different_selector {
        column-gap: 20px;
    }
    
Also, for now the parser still processes commented rules (likely to be fixed soon) .
The parser only processes linked stylesheets (link tag). Style elements, import directives and inline styles are ignored.
Be aware that the markup of your page is modified by the javascript, so it is possible that some CSS rules may not work after the multi-column layout is applied.
