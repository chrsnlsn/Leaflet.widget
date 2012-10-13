Leaflet.widget
==============

Provides a handler which binds a [Leaflet] map to a HTML element. GeoJSON data 
stored as text in the element will be parsed and added to the map. New features 
added to the map (via [Leaflet.draw], [Leaflet.paste], etc...) along with existing 
features can be encoded to GeoJSON and inserted into the bound HTML element 
with ```map.widget.write()```.

Includes [Leaflet.select]; a control extension for Leaflet.draw.  
Leaflet.select.js provides a 'selector' tool allowing one or many features to 
be selected. Actions can then be performed on selected features.

Implemented actions:
 - Remove features.

## Usage

To use:
1. Include an options object under a 'widget' property in your Leaflet 
   map's options. The object must contain a 'attach' property with its value being 
   an HTML element (or the id of one) to bind to.
2. Enable widget with ```widget.enable()```
3. When you're ready, write widget features to attached HTML element with ```widget.write```.

E.g:

```
// *.html
<form id='leaflet-widget-form'>
  <textarea id='leaflet-widget-input'> ... GeoJSON here ... </textarea>
  <input type='submit' />
</form>

// *.js
var form = L.DomUtil.get('leaflet-widget-form'),
    layer = L.tileLayer('http://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png'),
    map = L.map('map', {
            layers: [layer]
            widget: { attach: 'leaflet-widget-input' },
            select: true
          });

// It's important to enable the widget to ensure layers are added to the map.
map.widget.enable();

// Write widget features when form is submitted.
L.DomEvent.on(form, 'submit', map.widget.write, map.widget);
```

## Requires
- [Leaflet] - _Included in /lib._
- [Leaflet.draw] - _Included in /lib._

[Leaflet]: leaflet.cloudmade.com
[Leaflet.draw]: https://github.com/jacobtoye/Leaflet.draw
[Leaflet.paste]: https://github.com/thegreat/Leaflet.paste
[Leaflet.select]: https://github.com/thegreat/Leaflet.widget/blob/master/src/Leaflet.select.js
