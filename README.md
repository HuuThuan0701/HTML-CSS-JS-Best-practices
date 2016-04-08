# HTML/CSS Best Practices

## HTML

### Semantics

HTML5 provides us with lots of semantic elements aimed to describe precisely the content. Make sure you benefit from its rich vocabulary.

```html
<!-- bad -->
<div id="main">
  <div class="article">
    <div class="header">
      <h1>Blog post</h1>
      <p>Published: <span>21st Feb, 2015</span></p>
    </div>
    <p>…</p>
  </div>
</div>

<!-- good -->
<main>
  <article>
    <header>
      <h1>Blog post</h1>
      <p>Published: <time datetime="2015-02-21">21st Feb, 2015</time></p>
    </header>
    <p>…</p>
  </article>
</main>
```

Make sure you understand the semantics of the elements you're using. It's worse to use a semantic
element in a wrong way than staying neutral.

```html
<!-- bad -->
<h1>
  <figure>
    <img alt=Company src=logo.png>
  </figure>
</h1>

<!-- good -->
<h1>
  <img alt=Company src=logo.png>
</h1>
```

### Accessibility
Please remember to add ```alt``` property in any ```img``` tag. It will support our SEO process later.

```html
<!-- bad -->
<h1><img src="logo.png"></h1>

<!-- good -->
<h1><img src="logo.png" alt="Logo"></h1>
```

### Language

While defining the language and character encoding is optional, it's recommended to always declare
both at document level, even if they're specified in your HTTP headers. Favor UTF-8 over any other
character encoding.

```html
<!-- bad -->
<!doctype html>
<title>Hello, world.</title>

<!-- good -->
<!doctype html>
<html lang=en>
  <meta charset=utf-8>
  <title>Hello, world.</title>
</html>
```

### Use Practical ID & Class Values
Creating ID and class values can be one of the more difficult parts of writing HTML. These values need to be practical, relating to the content itself, not the style of the content. Using a value of red to describe red text isn’t ideal, as it describes the presentation of the content. Should the style of the text ever need to be changed to blue, not only does the CSS have to be changed, but so does the HTML in every instance where the class red exists.

The HTML here assumes that the alert message will be red. However, should the style of the alert change to orange the class name of red will no longer make sense and will likely cause confusion.

```html
<!-- bad -->
<p class="red">Error! Please try again.</p>

<!-- good -->
<p class="alert">Error! Please try again.</p>
```

### Using HTML Entities instead of characters


```html
<!-- bad -->
<div class="copyright">
    © 2016 Edental all rights reserved.
</div>

<!-- good -->
<div class="copyright">
    &copy; 2016 Edental all rights reserved.
</div>
```
 
### Performance

Unless there's a valid reason for loading your scripts before your content, don't block the
rendering of your page. If your style sheet is heavy, isolate the styles that are absolutely
required initially and defer the loading of the secondary declarations in a separate style sheet.
Two HTTP requests is significantly slower than one, but the perception of speed is the most
important factor.

```html
<!-- bad -->
<!doctype html>
<meta charset=utf-8>
<script src=analytics.js></script>
<title>Hello, world.</title>
<p>...</p>

<!-- good -->
<!doctype html>
<meta charset=utf-8>
<title>Hello, world.</title>
<p>...</p>
<script src=analytics.js></script>
```


## CSS

### Organize Code with Comments

CSS files can become quite extensive, spanning hundreds of lines. These large files can make finding and editing our styles nearly impossible. Let’s keep our styles organized in logical groups. Then, before each group, let’s provide a comment noting what the following styles pertain to.

Should we wish, we can also use comments to build a table of contents at the top of our file. Doing so reminds us—and others—exactly what is contained within the file and where the styles are located.

```css
/* bad */
header { ... }
article { ... }
.btn { ... }

/* good */
/* Primary header */
header { ... }

/* Featured article */
article { ... }

/* Buttons */
.btn { ... }
```

### Semicolons

While the semicolon is technically a separator in CSS, always treat it as a terminator.

```css
/* bad */
div {
  color: red
}

/* good */
div {
  color: red;
}
```

### Box model

The box model should ideally be the same for the entire document. A global
`* { box-sizing: border-box; }` is fine, but don't change the default box model
on specific elements if you can avoid it.

```css
/* bad */
div {
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
}

/* good */
div {
  padding: 10px;
}
```

### Specificity

Don't make values and selectors hard to override. Minimize the use of `id`'s
and avoid `!important`.

```css
/* bad */
.bar {
  color: green !important;
}
.foo {
  color: red;
}

/* good */
.foo.bar {
  color: green;
}
.foo {
  color: red;
}
```

### Overriding

Overriding styles makes selectors and debugging harder. Avoid it when possible.

```css
/* bad */
li {
  visibility: hidden;
}
li:first-child {
  visibility: visible;
}

/* good */
li + li {
  visibility: hidden;
}
```

### Use Shorthand Properties & Values

One feature of CSS is the ability to use shorthand properties and values. Most properties and values have acceptable shorthand alternatives. As an example, rather than using four different margin-based property and value declarations to set the margins around all four sides of an element, use one single margin property and value declaration that sets the values for all four sides at once. Using the shorthand alternative allows us to quickly set and identify styles.

When we’re only setting one value, though, shorthand alternatives should not be used. If a box only needs a bottom margin, use the margin-bottom property alone. Doing so ensures that other margin values will not be overwritten, and we can easily identify which side the margin is being applied to without much cognitive effort.

```css
/* bad */
img {
  margin-top: 5px;
  margin-right: 10px;
  margin-bottom: 5px;
  margin-left: 10px;
}
button {
  padding: 0 0 0 20px;
}

/* good */
img {
  margin: 5px 10px;
}
button {
  padding-left: 20px;
}
```

### Units

Use unitless values when you can. Favor `rem` if you use relative units. Prefer seconds over
milliseconds.

```css
/* bad */
div {
  margin: 0px;
  font-size: .9em;
  line-height: 22px;
  transition: 500ms;
}

/* good */
div {
  margin: 0;
  font-size: .9rem;
  line-height: 1.5;
  transition: .5s;
}
```

### Colors

If you need transparency, use `rgba`. Otherwise, always use the hexadecimal format.

```css
/* bad */
div {
  color: hsl(103, 54%, 43%);
}

/* good */
div {
  color: #5a3;
}
```

When available, use the three-character shorthand hexadecimal color value, and always use lowercase characters within any hexadecimal color value. The idea, again, is to remain consistent, prevent confusion, and embrace the syntax of the language the code is being written in.

```css
/* bad */
.module {
  background: #DDDDDD;
  color: #FF6600;
}

/* good */
.module {
  background: #ddd;
  color: #f60;
}
```


### Drawing

CSS3 is really good at drawing some simple shape. You can try to draw instead of using HTTP request for the image.

```css
/* bad */
div::before {
  content: url(white-circle.svg);
}

/* good */
div::before {
  content: "";
  display: block;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #fff;
}
```

### Modularize Styles for Reuse

CSS is built to allow styles to be reused, specifically with the use of classes. For this reason, styles assigned to a class should be modular and available to share across elements as necessary.

If a section of news is presented within a box that includes a border, background color, and other styles, the class of news might seem like a good option. However, those same styles may also need to be applied to a section of upcoming events. The class of news doesn’t fit in this case. A class of feat-box would make more sense and may be widely used across the entire website.

```css
/* bad */
.news {
  background: #eee;
  border: 1px solid #ccc;
  border-radius: 6px;
}
.events {
  background: #eee;
  border: 1px solid #ccc;
  border-radius: 6px;
}

/* good */
.feat-box {
  background: #eee;
  border: 1px solid #ccc;
  border-radius: 6px;
}
```
