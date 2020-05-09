---
layout: default
title: Markdown Cheatsheet
description: Syntax in how to write markdown file for this blog.
imgsrc: assets/pics/tools/markdown.jpg
banner: assets/pics/tools/markdown_banner.png
date: 2017-10-29
category: cheatsheet
tags: [Markdown,Cheatsheet]
author: Song Jiaming
extensions: ['extra', 'toc']
---
This is a summary of useful syntax (supported by this blog) to write Markdown :smile:

### __1. Headers__
`#`: h1 header, `##`: h2 header, ...,`#####`: h5 header, `######`: h6 header


### __2. Emphasis__
- Italics: `*asterisk*` - *asterisk*, or `_underscore_` - _underscore_
- Bold: `**asterisks**` - **asterisks** or `__underscores__` - __underscores__
- Strikethrough: `~~tildes~~` - ~~tildes~~
- Highlight or Inline code: `` which highlight text like the aboves did.


### 3. __Lists__
- Ordered list:
    1. First item `1. `
    2. Second item `2. `
    3. Third item `3. `

- Unordered lists:
    * You can use asterisk `*`
    * You can use minus `-` 
    * You can use plus `+`

#### Sublists
```
+ Normal lists with
    * `Tap` to create sublist
    - any combination works
```
+ Normal lists with
    * `Tap` to create sublist
    - any combination works


### __4. Links__
- `You can even have links: [Google](http://www.google.com)`: [Google](http://www.google.com)
- or just normal link: http://www.google.com

### __5. Images__
`![Markdown Logo](picture_link.jpg)`<br>

![Markdown Logo]({{site.baseurl}}/assets/pics/tools/markdown.jpg)

### __6. Code and Syntax Highlighting____

- Inline code (same as highlight):`var example = true`, use `
- This is a whole block code: Use ```
```
if (isAwesome){
  return true
}
```

- This is a whole block code with language specified:<br>
E.g. Use ```python 
```python
for i in range(10):
  print("hello world")
```

### __7. Tables__
```
| Right-Aligned | Center   | Left-Aligned |
| ------------: | :------: | :--------    |
| Apple         | Price    | $1600        |
| Pear          | Cost     |   $12        |
| Banana        | Profit   |    $1        |
```

| Right-Aligned      |  Center   | Left-Aligned |
| --------: | :-------: | :---- |
| Apple     | Price     | $1600 |
| Pear      | Cost      |   $12 |
| Banana    | Profit    |    $1 |

### __8. Blockquotes or indentation__
```
> First indentation
>> Further indentation
```
> First indentation
>> Further indentation


### __9. Math Environment__
Inline math: `\\(\frac{\pi}{2}\\)`,<br>
- This displays as \\(\frac{\pi}{2}\\)

or: `$\frac{x+y}{x^{2}}$`,<br>
- This displays as $\frac{x+y}{x^{2}}$

Alternatively, math can be written on its own line:

```
$$F(\omega) = \frac{1}{\sqrt{2\pi}} \int_{-\infty}^{\infty} f(t) \, e^{ - i \omega t}dt$$

\\[\int_0^1 f(t) \mathrm{d}t\\]

\\[\sum_j \gamma_j^2/d_j\\]
```

$$F(\omega) = \frac{1}{\sqrt{2\pi}} \int_{-\infty}^{\infty} f(t) \, e^{ - i \omega t}dt$$

\\[\int_0^1 f(t) \mathrm{d}t\\]

\\[\sum_j \gamma_j^2/d_j\\]

#### Coloring in math environment
Code `$\bbox[lightgreen]{\frac{1}{2}}$`<br>
Gives $\bbox[lightgreen]{\frac{1}{2}}$

#### Some special symbols that can just be copied used as text:
- arrows: →, ⇒, ⇔, ↔, ↓, ↑
- equations: ≤, ∈, ≡, ⊕, •
- logic: ∀, ∃, ∇
- letters: β, η, λ, Ω, 𝛿

For more 'copy and paste' math symbols , vistit http://math.typeit.org/


### __10. Horizontal Rule__
Three or more Hyphens `---` , Asterisks `***`, Underscores `___`

### __11. Task list__
```
1. [x] This is a complete item
2. [x] This is a complete item
3. [ ] this is a complete item
    - [ ] this is an incomplete item
    - [ ] this is an incomplete item
```

1. [x] This is a complete item
2. [x] This is a complete item
3. [ ] this is a complete item
    - [ ] this is an incomplete item
    - [ ] this is an incomplete item

### __12. Emoji__
Emoji shows up when `:tada:` -> :tada: , `:+1:` -> :+1: , `:heart:` -> :heart: ,etc

<br>

----
#### References
1. [Markdown Cheetsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
2. Sublime Markdown Cheetsheet