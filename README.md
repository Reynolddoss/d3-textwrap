d3textwrap
==========

<h3>IN A NUTSHELL</h3>

JavaScript plugin to enable automatic line wrapping in SVG images by using text, tspan, and foreignObject elements, as well as computed character length calculations. Include after D3 and call textwrap() on any text node in order to magically line wrap long strings of text to your desired boundaries in the SVG - safe, clean, and cross-browser!

--

<h3>IN A CONSIDERABLY LARGER NUTSHELL</h3>

<a href="http://d3js.org">D3.js</a> is an amazing library which can be used to build interactive information and art projects with data sets, JavaScript code, and scalable vector graphics rendered in the web browser. But it faces a very big problem: SVG images do not support line-wrapped text. At all! I know, I know, that's hard to believe, but it's true. This means that it can be very difficult to display longish chunks of text in SVG-based D3 projects.

The easiest way to deal with this is to first insert something called a foreignObject into the SVG, which is essentially a generic blob of space into which you can cram whatever else you want. Just initialize a foreignObject, insert a div tag or a p tag or whatever else, and let HTML handle the line wrapping just like it would on any web page.

Unfortunately <a href="http://stackoverflow.com/questions/19739672/foreignobject-is-not-working-in-ie10">Internet Explorer does not properly support foreignObject</a>. Surprise!

However, SVG does provide something called tspans, which are basically sub-nodes placed inside the text portion of the SVG which can be used to divide a longer string of text into smaller sections. This is even properly supported by Internet Explorer! It's still tough, though, because 1) neither SVG nor D3 give you an easy way to chop the longer text into the smaller segments, and 2) once you've done all your chopping you also have to position each tspan separately, and then 3) the method of positioning is slightly different depending on whether it's the first initial tspan or one that comes later in the set. It's a tremendous pain.

Even worse, there's a <a href="http://stackoverflow.com/questions/9137222/raphael-text-and-safari">silly</a> <a href="http://stackoverflow.com/questions/16701246/why-are-programmatically-inserted-svg-tspan-elements-not-drawn-except-with-d3">bug</a> in Safari wherein it doesn't support the dy attribute on tspans, which essentially just means that you can't vertically position them accurately. This includes Mobile Safari on iOS devices. In other words, if you use the foreignObject approach you're screwed on Internet Explorer, but if you use tspans you're screwed in Safari and on Apple mobile devices like iPhones and iPads. Those are all important browsers to support, and it's impossible to choose between them.

This plugin solves all the above problems. It first tests for foreignObject support and uses the simpler HTML option if it's available. If not, then it will fire a whole long sequence of tests to automatically split your text into whatever subsections will fit within the bounds you've specified, and then handles positioning of all the tspans for you. Safari gets foreignObjects, Internet Explorer gets tspans, all text wraps properly, and you get to go watch television and enjoy a snack instead of spending ages debugging this nonsense the way I did.

--

<h3>WITH MY SINCEREST REGRETS</h3>

The logic here works and has been battle-tested in a high-traffic public D3 infographic project, but the current implementation is still broken because I haven't fully converted it from the initial idiosyncratic version into a more flexible plugin. I'm working on it! In the meantime, feel free to holler at me at @vijithassar if you need help with this sort of thing.
