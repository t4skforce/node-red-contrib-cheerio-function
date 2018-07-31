<h1 align="center">Cheerio Function Node for Node-RED</h1>
<h5 align="center">Node-RED module cheerio a fast, flexible & lean implementation of core jQuery designed specifically for the server.</h5>

## Features
__&#10084; Familiar syntax:__
Cheerio implements a subset of core jQuery. Cheerio removes all the DOM inconsistencies and browser cruft from the jQuery library, revealing its truly gorgeous API.

__&#991; Blazingly fast:__
Cheerio works with a very simple, consistent DOM model. As a result parsing, manipulating, and rendering are incredibly efficient. Preliminary end-to-end benchmarks suggest that cheerio is about __8x__ faster than JSDOM.

__&#10049; Incredibly flexible:__
Cheerio wraps around @FB55's forgiving [htmlparser2](https://github.com/fb55/htmlparser2/). Cheerio can parse nearly any HTML or XML document.

## Cheerio is not a web browser

Cheerio parses markup and provides an API for traversing/manipulating the resulting data structure. It does not interpret the result as a web browser does. Specifically, it does *not* produce a visual rendering, apply CSS, load external resources, or execute JavaScript. If your use case requires any of this functionality, you should consider projects like [PhantomJS](http://phantomjs.org/) or [JSDom](https://github.com/tmpvar/jsdom).

## Example Flow
This example flow fetches the full download link for the latest android-sdk-tools for linux form the wepage.
![alt text](https://github.com/t4skforce/node-red-contrib-cheerio-function/raw/master/images/editor.png)
![alt text](https://github.com/t4skforce/node-red-contrib-cheerio-function/raw/master/images/example_flow.png)

```[{"id":"b6a346f6.e20ab8","type":"http in","z":"f4239029.65f45","name":"","url":"/android-sdk/latest","method":"get","upload":false,"swaggerDoc":"","x":120,"y":100,"wires":[["7c84616a.4312"]]},{"id":"8e1394d8.ff4f48","type":"http response","z":"f4239029.65f45","name":"","statusCode":"","headers":{"Content-Type":"application/json"},"x":810,"y":100,"wires":[]},{"id":"7c84616a.4312","type":"http request","z":"f4239029.65f45","name":"","method":"GET","ret":"txt","url":"https://developer.android.com/studio/","tls":"7434bd72.4c5b14","x":310,"y":100,"wires":[["fbbeb13d.ce447"]]},{"id":"fbbeb13d.ce447","type":"cheerio-function","z":"f4239029.65f45","name":"extract sdk-tools-linux","func":"msg.payload={url:$(\"a[href*='sdk-tools-linux']\")\n.attr(\"href\")};\nreturn msg;","outputs":1,"noerr":0,"x":520,"y":100,"wires":[["92a1a104.8b461"]]},{"id":"92a1a104.8b461","type":"json","z":"f4239029.65f45","name":"","property":"payload","action":"str","pretty":true,"x":690,"y":100,"wires":[["8e1394d8.ff4f48"]]},{"id":"204a6e81.d03bc2","type":"comment","z":"f4239029.65f45","name":"https://developer.android.com/studio/","info":"","x":160,"y":60,"wires":[]},{"id":"7434bd72.4c5b14","type":"tls-config","z":"","name":"NO Cert Check","cert":"","key":"","ca":"","certname":"","keyname":"","caname":"","verifyservercert":false}]```

## Usage
for detailed usage of cheerio head over to [github.com/cheeriojs](https://github.com/cheeriojs/cheerio).
