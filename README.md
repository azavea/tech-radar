# Motivation

At [Azavea](https://www.azavea.com/), we (hope someday to) maintain a [public Tech
Radar](http://azavea.github.io/tech-radar/) to help our engineering teams
align on technology choices. It is based on the [pioneering work
by ThoughtWorks](https://www.thoughtworks.com/radar).

This repository contains the code to generate the visualization:
[ `radar.js` ](/docs/radar.js) (based on [d3.js v4](https://d3js.org)).
Feel free to use and adapt it for your own purposes.

<img src="./images/tech-radar.png" height="400"/>

## Local Development

1. install dependencies with yarn (or npm):

``` 

yarn 
```

2. start local dev server:

``` 

yarn start
```

3. your default browser should automatically open and show the url

 

``` 

http://localhost:3000/
```

## Adding a new entry

If all you want to do is add a new entry, you'll need to create a javascript object like:

``` javascript
{
    quadrant: 0,
    ring: 2,
    label: "esbuild",
    active: true,
    link: null
}
```

Then put it in the appropriate quadrant. The quadrants we use are:

0. Development tools -- think things like `webpack`,        `sbt`,        `prettier`, etc.
1. Infrastructure -- this will largely include technology that either _is_ a cloud service, deploys cloud services, or makes working with cloud services easier
2. Frameworks -- these are ways of doing big technical tasks. For example, React is a framework for frontend applications, Http4s is a framework for backend applications, and tapir is a framework for keeping backend applications and docs in sync.
3. Geospatial data -- this quadrant includes ways of organizing, visualizing, and storing geospatial data.

Add your entry to the appropriate array -- one of `devToolingEntries` , `dataManagementEntries` , `infrastructureEntries` , or `frameworkEntries` .

## Creating a new tech radar

If you're interested in starting from scratch, you can follow the following steps:

1. include `d3.js` and `radar.js`:

``` html
<script src="https://d3js.org/d3.v4.min.js"></script>
<script src="http://zalando.github.io/tech-radar/release/radar-0.5.js"></script>
```

2. insert an empty `svg` tag:

``` html
<svg id="radar"></svg>
```

3. configure the radar visualization:

``` js
radar_visualization({
    svg_id: "radar",
    width: 1450,
    height: 1000,
    colors: {
        background: "#fff",
        grid: "#bbb",
        inactive: "#ddd"
    },
    title: "My Radar",
    quadrants: [{
            name: "Bottom Right"
        },
        {
            name: "Bottom Left"
        },
        {
            name: "Top Left"
        },
        {
            name: "Top Right"
        }
    ],
    rings: [{
            name: "INNER",
            color: "#93c47d"
        },
        {
            name: "SECOND",
            color: "#b7e1cd"
        },
        {
            name: "THIRD",
            color: "#fce8b2"
        },
        {
            name: "OUTER",
            color: "#f4c7c3"
        }
    ],
    print_layout: true,
    entries: [{
            label: "Some Entry",
            quadrant: 3, // 0,1,2,3 (counting clockwise, starting from bottom right)
            ring: 2, // 0,1,2,3 (starting from inside)
            moved: -1 // -1 = moved out (triangle pointing down)
            //  0 = not moved (circle)
            //  1 = moved in  (triangle pointing up)
        },
        // ...
    ]
});
```

Entries are positioned automatically so that they don't overlap.

As a working example, you can check out `docs/index.html` &mdash; the source of our [public Tech
Radar](http://zalando.github.io/tech-radar/).

## License

``` 

The MIT License (MIT)

Copyright (c) 2017 Zalando SE

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
```
