---
layout: post
hide: True
title: Basics of HTML Guide
description: An introduction to basic HTML, and resources to learn more.
type: ccc
permalink: /basics/html
author: Rohan Juneja
---

{% include nav_basics.html %}


# How does HTML work?
Similar function to Markdown, syntax defines how stuff should be displayed
- HTML is based on beginning and closing tags `<tagname>content</tagname>`
  - Note the "/" on the ending or closing tag of the pair

## Compare markdown to html below
This below example shows comparison of a [heading](https://www.w3schools.com/html/html_headings.asp) and [paragraph](https://www.w3schools.com/html/html_paragraphs.asp).  Click on links to see many more HTML examples.


```python
%%markdown

### Markdown: This is a Heading

This is a paragraph

```



### Markdown: This is a Heading

This is a paragraph




```python
%%html

<h3>HTML: This is a Heading</h3>
<p>This is a paragraph.</p>
```



<h3>HTML: This is a Heading</h3>
<p>This is a paragraph.</p>



# Attributes
- Learn about [attributes](https://www.w3schools.com/html/html_attributes.asp) 
- Tags can have additional info in the form of attributes
- Attributes usually come in name/value pairs like: name="value"

```html
<tagname attribute_name="attribute_value" another_attribute="another_value">inner html text</tagname>
```

- href example with attribute for web link and inner html to describe link

```html
<a href="https://www.w3schools.com/html/default.asp">Visit W3Schools HTML Page</a>
```

## Sample Markdown vs HTML Tags
Image Tag - Markdown

```md
![describe image](link to image)
```

Image Tag - HTML

```html
<!-- no content so no end tag, width/height is optional (in pixels) -->
<img alt="describe image" src="link to image" width="100" height="200">
```

Link Tag - Markdown

```md
[link text](link)
```

Link Tag - HTML

```html
<a href="link">link text</a>
```

Bolded Text - Markdown

```md
**Bolded Text**
```

Bolded Text - HTML

```md
<strong>Bolded Text</strong>
```

Italic Text - Markdown

```md
*Italic Text*
```

Italic Text - HTML

```md
<i>Italic Text</i>
```

# More tags (not really in markdown)
P tag (just represeants a paragraph/normal text)

```html
<p>This is a paragraph</p>
```

Button

```html
<button>some button text</button>
```

Div (groups together related content)

```html
<!-- first information -->
<div>
    <!-- notice how tags can be put INSIDE eachother -->
    <p>This is the first paragarph of section 1</p>
    <p>This is the second paragraph of section 1</p>
</div>

<!-- second information -->
<div>
    <!-- notice how tags can be put INSIDE eachother -->
    <p>This is the first paragarph of section 2</p>
    <p>This is the second paragraph of section 2</p>
</div>
```



# Resources
- https://www.w3schools.com/html/default.asp
- I will show a demo of how to find information on this website

# HTML Hacks
- Below is a wireframe for an HTML element you will create. A wireframe is a rough visual representation of HTML elements on a page and isn't necessarily to scale or have the exact styling that the final HTML will have. Using the syntax above, try to create an HTML snippet that corresponds to the below wireframe.
- The "a tags" can contain any links that you want

![wireframe for html hacks]({{ site.baseurl }}/images/wireframe.png)


```python
%%html

<!-- put your HTML code in this cell, Make sure to press the Run button to see your results below -->
```



<!-- put your HTML code in this cell, Make sure to press the Run button to see your results below -->


