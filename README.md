# typewrite

A javascript typewriter library which animates the **typing**, **deleting**, and **selecting** of text on a page

<img src="https://raw.githubusercontent.com/mrvautin/typewrite/master/typewrite.gif" width="640">

### Demo
See [here](https://rawgit.com/mrvautin/typewrite/master/index.html "Demo").

### Installation

`typewrite` is a jQuery plugin, so it needs to be included in your HTML after jQuery. e.g:

From CDN:
``` javascript
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/socialjazz/typewrite/dist/typewrite.min.js"></script>
```

Setup your target element to type into:

``` html
<div id="typewriteText"></div>
```

Some `typewrite` demo actions with default settings:

``` javascript
$(document).ready(function(){
    $('#typewriteText').typewrite({
        actions: [
            {type: 'Hello. '},
            {type: '<br>'},
            {type: 'Weclome '},
            {delay: 1500},
            {remove: {num: 1, type: 'stepped'}},
            {select: {from: 11, to: 16}},
            {delay: 2000},
            {remove: {num: 5, type: 'whole'}},
            {delay: 300},
            {type: 'lcome to typewrite. '},
            {type: '<br>'},
            {type: 'It\'s just so easy to setup and use.'}
        ]
    });
});
```

### Using typewrite

`typewrite` works on actions. You pass an array of actions which will be executed in order. See example above.

### actions

`typewrite` can add text, delay (pause), remove text and even select text.

#### Typing

Adding text is done by passing an object with a key of `type` and a value of the text you would like typed. e.g:

``` javascript
{type: 'Hello.'}
```

#### Remove

Removing text is done by passing a nested object with a key of `remove` and a nested object with the number of characters and the type of remove.

To remove 5 characters, one character at a time:

``` javascript
{remove: {num: 5, type: 'stepped'}}
```

To remove 5 characters, in one whole remove:

``` javascript
{remove: {num: 5, type: 'whole'}}
```

Note: Generally you might want to use the `whole` remove after you have selected some text

#### Select

Selecting text is done by passing a nested object with a key of `select` and a nested object with the index of characers you want to select.

The following will select from the 11th character to the 16th:

``` javascript
{select: {from: 11, to: 16}}
```

#### Delay (pause)

Delay (pause) is done by passing an object with a key of `delay` and a value with the amount of time in milliseconds to delay or pause.

The following will delay for 1500 milliseconds (1.5 seconds).

``` javascript
{delay: 1500}
```

#### Speed

You can change the typing speed midway through the actions by passing an object with a key of `speed` and a value with the amount of characters per second.

The following will change the typing speed to 22 characters per second.

``` javascript
{speed: 22}
```

### Options

**speed** {integer}: Characters per second - Default: `12`

**blinkSpeed** {integer}: Blinks per second of cursor - Default: `2`

**showCursor** {boolean}: Whether to show the cursor - Default: `true`

**blinkingCursor** {boolean}: Whether the cursor blinks - Default: `true`

**cursor** {string}: The cursor character - Default: `'|'`

**selectedBackground** {string}: The Hex color value of the selected background - Default: `'#6EC4FF45'`

**selectedText** {string}: The Hex color value of the selected text - Default: `'initial'`

**continuous** {boolean}: Whether to run on continuous loop - Default: `false`

Providing option are done by setting the object with the actions. Eg:

``` javascript
$('#typewriteText').typewrite({
    blinkSpeed: 15,
    cursor: '@',
    actions: [
        {type: 'Hello. '},
        {type: '<br>'},
        {type: 'Weclome '},
        {delay: 1500},
        {remove: {num: 1, type: 'stepped'}},
        {select: {from: 11, to: 16}},
        {delay: 2000},
        {remove: {num: 5, type: 'whole'}},
        {delay: 300},
        {type: 'lcome to `typewrite`. '},
        {type: '<br>'},
        {type: 'It\'s so easy to setup and use.'}
    ]
});
```

### Styling

If you want to add additional CSS to further style `typewrite`, please use the following CSS classes:

`.blinkingCursor` is the class applied to the blinking cursor (if enabled)

`.typewriteSelected` is the class applied to the selected text. You may want to add CSS rather then setting the `selectedBackground` and `selectedText` values.

### Events

`typewrite` supports the use of events for all the actions. Some actions trigger returned data and some don't, see below for examples:

``` javascript
$('#typewriteText')
    .on('typewriteStarted', function() {
        console.log('typewrite has started');
    })
    .on('typewriteComplete', function() {
        console.log('typewrite has complete');
    })
    .on('typewriteTyped', function(event, data) {
        console.log('typewrite has typed', data);
    })
    .on('typewriteRemoved', function(event, data) {
        console.log('typewrite has removed', data);
    })
    .on('typewriteNewLine', function() {
        console.log('typewrite has added a new line');
    })
    .on('typewriteSelected', function(event, data) {
        console.log('typewrite has selected text', data);
    })
    .on('typewriteDelayEnded', function() {
        console.log('typewrite delay has ended');
    })
    .typewrite({
        actions: [
            {type: 'Hello. '},
            {type: '<br>'},
            {type: 'Weclome '},
            {delay: 1500},
            {remove: {num: 1, type: 'stepped'}},
            {select: {from: 11, to: 16}},
            {delay: 2000},
            {remove: {num: 5, type: 'whole'}},
            {delay: 300},
            {type: 'lcome to typewrite. '},
            {type: '<br>'},
            {type: 'It\'s just so easy to setup and use.'}
        ]
    });
```