---
layout: post
author: Juande Santander-Vela
title:  "Including HTML code in page, and also show its content verbatim"
date:   2021-05-05 12:48:30 -0400
categories: [html, javascript, jQuery, "code display"]
---

I was asked by a colleague at SKAO how to render part of an HTML page in verbatim, while the code existed there.

I started from this [solution in StackOverflow to the question *How to include verbatim source code into an html document*][1]:

[1]: https://stackoverflow.com/questions/40445310/how-to-include-verbatim-source-code-into-an-html-document "How to include verbatim source code into an html document"

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Page that includes things</title>
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
        <script>
            $.ajax({
              url : "./included.html",
              dataType: "text",
              success : function (data) {
                $("#verbatim_includedhtml").text(data);
                $("#verbatim_includedhtml").before(data);
              }
            });
        </script>
    </head>
    <body>
        <div id="verbatim_includedhtml"></div>
    </body>
</html>
```

The first `<script>` loads jQuery. The second `<script>`:

 * loads the content of file `included.html`
 * uses jQuery to find the tag with `id` equal to `verbatim_includedhtml`, and injects the file into it.
 * uses jQuery again to prepend (`.before`) the HTML to it.
    
After loading the page, and running that script, this is the resulting HTML:

```html
    <!DOCTYPE html>
    <html>
        <head>
            <title>Page that includes things</title>
            <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
            <script>
                $.ajax({
                  url : "./included.html",
                  dataType: "text",
                  success : function (data) {
                    $("#verbatim_includedhtml").text(data);
                    $("#verbatim_includedhtml").before(data);
                  }
                });
            </script>
        </head>
        <body>
            <div id="my_snippet">
                <p>
                    This is the code, <em>you see</em>? It should be yours
                </p>
                <ul>
                    <li>List item 1
                    </li>
                    <li>List item 2
                    </li>
                </ul>
            </div>
            <div id="verbatim_includedhtml">
                "<div id="my_snippet">
                    <p>
                        This is the code, <em>you see</em>? It should be yours
                    </p>
                    <ul>
                        <li>List item 1
                        </li>
                        <li>List item 2
                        </li>
                    </ul>
                </div>"
            </div>
        </body>
    </html>
```

Where the original content in `included.html` is shown from `<div id="my_snippet">` till the end of that `<div>`.

My colleague finally decided to go with a [similar solution][2], taking the content from the page itself. I tried to reproduce this approach, and this is the raw HTML that I came out with:

[2]: https://jsfiddle.net/wphps3od/ "JSFiddle playground: displaying verbatim code from a tag"

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Page that includes things</title>
        <script>
            document.addEventListener('readystatechange', event => { 
                // this is the event handler for when the page has loaded 
                if (event.target.readyState === "complete") {
                    // get the internal HTML inside the element with id `myCode`
                    var a = document.getElementById("myCode").innerHTML;
                    // do a manual split of the tags
                    var b = a.split('>');

                    for (var i = 0; i < b.length; i++) {
                      // reconstruct the bracket
                      var replaceBracket = i == b.length - 1 ? "" : ">";
                      // add each tag one by one inside the textContent
                      document.getElementById("loadHere").textContent += b[i] + replaceBracket + " \r\n";
                    }
                }
            });
        </script>
    </head>
    <body>
        <div id="myCode">
        <!-- This is the code to be reproduced -->
            <p>
                hello world
            </p>
        </div>
        <div id="loadHere" style="white-space: pre;"></div>
    </body>
</html>
```

After loading it in the browser, the HTML becomes:

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Page that includes things</title>
        <script>
            document.addEventListener('readystatechange', event => { 
                // this is the event handler for when the page has loaded 
                if (event.target.readyState === "complete") {
                    // get the internal HTML inside the element with id `myCode`
                    var a = document.getElementById("myCode").innerHTML;
                    // do a manual split of the tags
                    var b = a.split('>');

                    for (var i = 0; i < b.length; i++) {
                      // reconstruct the bracket
                      var replaceBracket = i == b.length - 1 ? "" : ">";
                      // add each tag one by one inside the textContent
                      document.getElementById("loadHere").textContent += b[i] + replaceBracket + " \r\n";
                    }
                }
            });
        </script>
    </head>
    <body>
        <div id="myCode">
        <!-- This is the code to be reproduced -->
            <p>
                hello world
            </p>
        </div>
        <div id="loadHere" style="white-space: pre;">
            <!-- This is the code to be reproduced -->
        
            <p>
                hello world
            </p>
        </div>
    </body>
</html>
```

Which, as you can see, even reproduces the comment (which is not displayed inside `<div id="myCode">`).

pps. By the way, welcome back to this blog!