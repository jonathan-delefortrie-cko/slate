---
title: CKO Graph Documentation

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

search: true
---

# Introduction

> Set the library on the document:

```html
<script src="./d3.v3.min.js"></script>
<script src="./CKOGraph.min.js"></script>
```

Welcome to the CKO Graph Library !!!

The current version of the library is implementing two types of graph. (Line Chart/Bar Chart)  
The Library contain three differents class (TooltipPublisher/ChartStorage/Render).  
The CHECKOUT is the main class to handle all of those.  

Please see the following parts below to have a global view on how to use the library.

# Instantiate

> Instantiation with the minimum variable:

```javascript
var cko = CKOGRAPH.createChart(); // Line Chart
var cko = CKOGRAPH.createChart('Bar'); // Bar Chart
var cko = CKOGRAPH.createChart('Line'); // Line Chart
```

> Instantiation with the maximum variable:

```javascript

var data = []; // Array contening the plot x and y : [x,y]
var id = 'myId'; // Necessary to remove a plot dynamicaly
var color = '#fffeee'; // Color hexadecimal

var options = {
    element: 'myContainer'
    ticks: 5,
    dateFormat: '%a %d %H:%M:%S',
    width: null,
    height: null,
    background: true,
    axes: {
        xAxis: {
            visible: true,
            height: 45,
            padding: 0
        },
        yAxis: {
            visible: true,
            height: 65,
            padding: 25
        }
    }
};

var cko = CKOGRAPH.createChart('Line',data,id,color,options);
```

The defaults options are set on the current design of Checkout.
please, feel free to arrange the graph as you need.

### Instance parameters

Parameter | Type | Description
--------- | ------- | -----------
data | array | Data is an optional parameters, by setting this you start automatically the render.
id | string | Id is an optional parameters, usefull to handle the plot.
color | array | Color is an optional parameters associated to the plot.
options | object | Override the default value, see the structure below.

### Optional attributes

Attribute | Type | Description
--------- | ---- | -----------
element | string | The string should be an id, otherwise we set the parent element by default.
ticks | number | Divisor for the Y axis, useful to minimize the render.
dateFormat | string | The date format option is based on the d3 js Library.
width | number/null | The null value give automatically the parent size.
height | number/null | The null value give automatically the parent size.
background | true/false | Background state.
axes.(x/y)Axis.visible | true/false | Axis state.
axes.(x/y)Axis.height | number | Axis size : Weight of the axis.
axes.(x/y)Axis.padding | number | Axis padding : Where start and stop the axis.

`* A default color is set automatically if the parameters is missing during the plot installation`

<aside class="notice">
Id, data and color are associated please be aware by passing a color parameters you must have a data associate. Otherwise the parameter itself is useless.
</aside>

# Methods

> Some examples of methods:

```javascript
cko.addElement(id,data,color); // Increment the graph with a new plot (line/bar)
cko.removeElement(id); // Remove the plot by its id

cko.showBackground();
cko.hideBackground();

cko.setWidth();
cko.setHeight();

cko.clear(); // Clear storage
cko.refresh(); // Redraw entirely the canvas
```

Those chain methods useful to edit the graph after the first loading.

### Chain methods

Method | Parameters | Description
------ | ---------- | -----------
addElement | id/data/color | Method to add a plot.
removeElement | id/data/color | Method to remove the plot by id.
showBackground | empty | Display the background.
hideBackground | empty | Hide the the background.
setWidth | number | Resize the width and force it width.
setHeight | number | Resize the height and force it height.
clear | object | Clear entirely the graph / remove all the plots.
refresh | object | Redraw the canvas based on the actuel values.

`* Use the refresh method and pass the parameters in it if you want change entirely the design`

<aside class="success">
By passing the optional object parameters in the cleaner and refresh method it will redraw the canvas based on the new parameters dynamically.
</aside>

<aside class="notice">
You must know by each call of a method you automatically refresh the canvas. You can potentially reset the options object and push it in the refresh method to minimize its the time render.
</aside>

# Data

The format data is an array which contain arrays with date and value for each entry. It is possible to add the hours in the date for more precision. See the following examples.

### Format of data

Entry | Axis | Type
----- | ---- | ----
1 | x | date
2 | y | value

`* The first entry should be a timestamp format`

> Here is the array needed:

```array
[
  ["03/21/2013", "12"],
  ["03/22/2013", "14"],
  ["03/23/2013", "15"],
  ["03/24/2013", "14"],
  ["03/25/2013", "18"],
  ["03/26/2013", "19"],
  ["03/27/2013", "20"],
  ["03/28/2013", "21"],
  ["03/29/2013", "22"],
  ["03/30/2013", "10"],
  ["03/31/2013", "11"]
]
```

> Example with hour:

```array
[
  ["03/21/2013 00:00:00", 12],
  ["03/21/2013 01:00:00", 14],
  ["03/21/2013 02:00:00", 15],
  ["03/21/2013 03:00:00", 14],
  ["03/21/2013 04:00:00", 18],
  ["03/21/2013 05:00:00", 19],
  ["03/21/2013 06:00:00", 20],
  ["03/21/2013 07:00:00", 21],
  ["03/21/2013 08:00:00", 22],
  ["03/21/2013 09:00:00", 10],
  ["03/21/2013 10:00:00", 11],
  ["03/21/2013 11:00:00", 12],
  ["03/21/2013 12:00:00", 14],
  ["03/21/2013 13:00:00", 15],
  ["03/21/2013 14:00:00", 14],
  ["03/21/2013 15:00:00", 18],
  ["03/21/2013 16:00:00", 19],
  ["03/21/2013 17:00:00", 20],
  ["03/21/2013 18:00:00", 21],
  ["03/21/2013 19:00:00", 22],
  ["03/21/2013 20:00:00", 10],
  ["03/21/2013 21:00:00", 11],
  ["03/21/2013 22:00:00", 11],
  ["03/21/2013 23:00:00", 21]
]
```

<aside class="warning">
Be aware that graph is a timeline of values given. The first column of this array should be the data with a date-time format and the second one the value.
</aside>