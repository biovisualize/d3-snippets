#A collection of D3.js snippets and related tools

### *Notation for SVG path*

```javascript
    selection.append('path')
        .attr({
            d: 'M' + [[0, 0], [width, 0]]
        });
```

### *Toggle class*

```javascript
    selection.classed('highlighted', !selection.classed('highlighted'));
```

### *SVG to PNG*

```javascript
    var svgString = new XMLSerializer().serializeToString(document.querySelector('svg'));
    var canvas = document.getElementById("canvas");
    var ctx = canvas.getContext("2d");
    var DOMURL = self.URL || self.webkitURL || self;
    var img = new Image();
    var svg = new Blob([svgString], {type: "image/svg+xml;charset=utf-8"});
    var url = DOMURL.createObjectURL(svg);
    img.onload = function() {
        ctx.drawImage(img, 0, 0);
        var png = canvas.toDataURL("image/png");
        document.querySelector('#png-container').innerHTML = '<img src="'+png+'"/>';
        DOMURL.revokeObjectURL(png);
    };
    img.src = url;
```

So you can also grab the SVG as a string from the browser console:

```javascript
    new XMLSerializer().serializeToString(document.querySelector('svg'))
```

### *Append HTML to node*
Works for HTML as well as SVG

```javascript
function appendHtmlToNode(htmlString, parent){
    return parent.appendChild(document.importNode(new DOMParser().parseFromString(htmlString, 'text/html').body.childNodes[0], true));
}

var fooNode = appendHtmlToNode('<div class="foo"></div>', node);
```