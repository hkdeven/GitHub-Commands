# github-markdown-tricks

Github allows us to use a limited subset of HTML in our Markdown files – lets see what mischief we can do with that!

## Alignment

<div align="center">This is center aligned!</div>
<div align="left">Left aligned</div>
<div align="right">Right aligned</div>

```HTML
<div align="center">This is center aligned!</div>
<div align="left">Left aligned</div>
<div align="right">Right aligned</div>
```

## Hanging indendation

<dl>
  <dt>This is a list</dt>
  <dd>With hanging indentation</dd>

  <dt>Another list item</dt>
  <dd>With some description that might wrap over more than one line hopefully. This is to showcase that the hanging indentation persists even with a very long description and a bunch of line breaks!</dd>
</dl>

```HTML
<dl>
  <dt>This is a list</dt>
  <dd>With hanging indentation</dd>
</dl>
```
