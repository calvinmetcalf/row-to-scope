# Row-to-Scope

## Concept

If you can write HTML, you can put all of your data records online! Row-to-Scope paints
over the page for every row in your data.

* /row?page=1 is a page with the first row's data
* /row?page=2 is a page with the second row's data
* /row?page=3 is a page with the third row's data
* ...

### Key Components

* The row/index.html page is how the page looks for the first row in your data.

* data/data.csv is a spreadsheet of your data. Use CSV, KML, GeoJSON, or shapefiles.

* The index.html page is a homepage for your app. Use it for important information and links.

### More Detailed Info

* To change from data/data.csv to data/data.geojson or another file, add a tag just above the &lt;script&gt; tag for row-to-scope.js

    &lt;script type="text/javascript"&gt;var dataSource = "data/geojson.geojson";&lt;/script&gt;

* Put JavaScript code that runs after the correct row is loaded inside an init() function.

* In JavaScript, replaceRow( "NAME" ) will convert a value in the first row to a value from the requested row

* replaceRow also replaces numbers, arrays, and JSON objects from the first row.

* jQuery functions $.html and $.text will automatically replace values from the first row.

* For all geo formats, use getGeometry() to return a GeoJSON feature (including geometry and properties). For example, with Leaflet:

      L.geoJson( getGeometry() ).addTo(map);
    
or, to be more detailed and include replaceRow

      L.geoJson( getGeometry(), {
        onEachFeature: function(feature, layer){
          layer.bindPopup( replaceRow("60647") );
        }
      }).addTo(map);

* The previous(), next(), first(), and last() functions let you page through the rows.

### Tips

* The user downloads the whole database every time that they visit a page! Don't use this for many thousands of rows.

* Fill the first row or feature with column names like {{NAME}}, {{DESCRIPTION}}, {{HEIGHT}} so that it's easier to write your template page. /row?page=1 will be template, but the rest will have your data.

* Put &lt;script&gt; and &lt;style&gt; tags in the &lt;head&gt; of the page.

* For complex maps, 3D pointclouds, and other large datasets, place those files in the /data folder. List a file name ("row1.geojson", "row2.geojson", etc.) in your data.csv, so your page loads only one of these large datasets and not the complete set for each row. Use <a href="https://github.com/mapmeld/row-to-scope/tree/gh-pages/demos/webgl/data">the WebGL example</a> as a guide.

* (Future) If you have a meaningful ID for each row, use an {{ID}} column in a CSV, or ID property to a GeoJSON. Then link to pages using /row?id=SPECIAL_ID

## Supported Formats

* CSV
* GeoJSON
* Google Earth KML
* Shapefile using <a href="https://github.com/calvinmetcalf/shapefile-js">shapefile-js</a>

## Consider Jekyll or Sheetsee

If you want to
<a href="http://jekyllrb.com/">build blogs and no-CMS websites</a> or
<a href="http://jlord.github.io/sheetsee.js/">visualize data from Google Spreadsheets</a>,
there are much better tools to do that!

Row-to-Scope is just designed to be as simple as possible.

