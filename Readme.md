# Express Messages

The _express-messages_ module provides flash notification rendering.

### Express 2.x

To use simply assign it to a dynamic helper:

    app.dynamicHelpers({ messages: require('express-messages') });

### Express 3+

Install [connect-flash](https://github.com/jaredhanson/connect-flash) and add them as middleware:

```
app.use(require('connect-flash')());
app.use(function (req, res, next) {
  res.locals.messages = require('express-messages')(req, res);
  next();
});
```

## Installation

    $ npm install express-messages

## Usage

On the server, add messages like this:

    req.flash("info", "herp derp %s", something)

Then in a view you may output the notifications based on your templating engine:

### [EJS](https://github.com/visionmedia/ejs)

    <%- messages() %>

### [Jade](http://jade-lang.com/)

    != messages()

Which outputs HTML as shown below:

    <div id="messages">
      <ul class="info">
        <li>Email queued</li>
        <li>Email sent</li>
      </ul>
      <ul class="error">
        <li>Email delivery failed</li>
      </ul>
    </div>

## Using a custom template

Alternatively, you can specify a custom template (a file in the views directory of your [Express](http://expressjs.com) app) and locals:

### [EJS](https://github.com/visionmedia/ejs)

    <%- messages('myTemplate', locals) %>

### [Jade](http://jade-lang.com/)

    != messages('myTemplate', locals)

The template will receive an object called `messages` of the form

    {
      "info" : [
        "Email queued",
        "Email sent"
      ],
      "error": [
        "Email delivery failed"
      ]
    }
For example, the HTML above can be produced with the following Jade template:

    .messages
      each type in Object.keys(messages)
        ul(class="#{type}")
          each message in messages[type]
            li= message

## Running Tests

    $ npm test

## License

(The MIT License)

Copyright (c) 2010 TJ Holowaychuk &lt;tj@vision-media.ca&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
