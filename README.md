# fluid.scss

*fluid.scss* is a [Sass](http://sass-lang.com/)-based, [BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)-aware, completely customizable fluid widths and breakpoint system. It works in IE8+ and it's inspired by the idea behind the widths system of [csswizardy-grids](https://github.com/csswizardry/csswizardry-grids).

## Configuation

### Classes

#### `$use-classes`

If this is set to `true`, classes will be used in the generated code instead of placeholder selectors.

### Breakpoints

#### `$breakpoints`

The default breakpoints used through out the system.

#### `$default-widths`

The default widths used through out the system.

#### `$palm-widths`, `$lap-widths` and `$desk-widths`

The widths used for a specific breakpoint. These can be renamed to anything you want, but the names should match the names of the breakpoints in the `$breakpoints` variable.

## Usage

### `fluid-widths`

~~~ scss
@include fluid-widths($breakpoint, $widths, $helpers);
~~~

The `$breakpoint` parameter needs to match the one defined in the `$breakpoints` variable (or `default` if you want to generate your default widths), the `$widths` parameter the relevant widths for your breakpoint and the `$helpers` parameter should be set to either `hide`, `show`, `both` or `none`.

### `fluid-point`

~~~ scss
@include fluid-point($breakpoint) {
  // ...  
};
~~~
The `$breakpoint` parameter needs to match the one defined in the `$breakpoints` variable.

## Examples

### `fluid-widths`

#### Regular classes

##### Variables

~~~ scss
$breakpoints: (
  ("palm", "(max-width: 480px)"),
  ("lap", "(min-width: 481px) and (max-width: 1023px)")
);

$default-widths: (
  ("one-whole", "100%"),
  ("three-quarters", "75%"),
  ("two-thirds", "66.666%"),
  ("one-half", "50%"),
  ("one-third", "33.333%"),
  ("one-quarter", "25%"),
);

$palm-widths: (
  ("one-whole", "100%"),
  ("one-half", "50%")
);

$lap-widths: (
  ("one-whole", "100%"),
  ("three-quarters", "75%"),
  ("one-half", "50%"),
  ("one-quarter", "25%")
);
~~~

##### Mixins

~~~ scss
@include fluid-widths("default", $default-widths, "none");
@include fluid-widths("lap", $lap-widths, "none");
@include fluid-widths("palm", $palm-widths, "hide");
~~~

##### Markup

~~~ html
<div class="one-half  lap--one-whole  palm--hide">
  <!-- ... -->
</div>
~~~

#### Placeholder selectors

##### Variables

~~~ scss
$breakpoints: (
  ("palm", "(max-width: 480px)"),
  ("lap", "(min-width: 481px) and (max-width: 1023px)")
);

$default-widths: (
  ("one-whole", "100%"),
  ("three-quarters", "75%"),
  ("two-thirds", "66.666%"),
  ("one-half", "50%"),
  ("one-third", "33.333%"),
  ("one-quarter", "25%"),
);

$palm-widths: (
  ("one-whole", "100%"),
  ("one-half", "50%")
);

$lap-widths: (
  ("one-whole", "100%"),
  ("three-quarters", "75%"),
  ("one-half", "50%"),
  ("one-quarter", "25%")
);
~~~

##### Mixins

~~~ scss
@include fluid-widths("default", $default-widths, "none");
@include fluid-widths("lap", $lap-widths, "none");
@include fluid-widths("palm", $palm-widths, "hide");
~~~

##### SCSS

~~~ scss
.content {
  @extend %one-half;
  @extend %lap--one-whole;
  @extend %palm--hide;
}
~~~

##### Markup

~~~ html
<div class="content">
  <!-- ... -->
</div>
~~~

### `fluid-point`

#### SCSS

~~~ scss
@include fluid-point("palm") {
  body {
    color: red;
  }
}

body {
  @include fluid-point("lap") {
    color: blue;
  }
}
~~~

## Limitations

In every variable list (ie: `$breakpoints`, `$default-widths` and the like) there has to be *atleast* two values set. This is due to a limitation in Sass where this:

~~~ scss
$list: (
  ("foo", "bar")
);
~~~

Returns the same list index as this:

~~~ scss
$list: (
  ("foo", "bar"),
  ("foo", "bar")
);
~~~

Another issue is that in the former the item index (`nth`) is only one, while in the latter it's two. Since you can't (atleast to my knowledge) check the length of that particular index there's not much that can be done about it, I'm afraid.

If you *really* don't want to generate more classes than necessary, you could use the `fluid-point` mixin and write them manually, like this:

~~~ scss
@include fluid-point("palm") {
  .palm--one-whole {
    width: 100%;
  }
}
~~~

## License

The MIT License (MIT)

Copyright (c) 2013 Ellen Gummesson

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
