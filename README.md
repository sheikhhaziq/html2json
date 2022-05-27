# html2json & json2html

## How to use

### browser

include htmlparser.js & html2json.js scripts:

```html
<script src="src/htmlparser.js"></script>
<script src="src/html2json.js"></script>
```



### API

```javascript
json = html2json(document.body.innerHTML);
html = json2html(json);

console.assert(json === html);
```


### JSON format

every json has `node`

members of `node` are

- `root`
- `element`
- `text`
- `comment`

`root` node is the root of JSON, every JSON must have only one root `root`, could have `child`.

`element` node represents html element, could have `tag`, `attr`, `child`.

`text` node represents text element, could have `text`.

`comment` node represents commment element, could have `text`.


### Sample

html:

```html
<div id="1" class="foo">
<h2>sample text with <code>inline tag</code></h2>
<pre id="demo" class="foo bar">foo</pre>
<pre id="output" class="goo">goo</pre>
<input id="execute" type="button" value="execute"/>
</div>
```

json:

```javascript
{
  node: 'root',
  child: [
    {
      node: 'element',
      tag: 'div',
      attr: { id: '1', class: 'foo' },
      child: [
        {
          node: 'element',
          tag: 'h2',
          child: [
            { node: 'text', text: 'sample text with ' },
            { node: 'element', tag: 'code', child: [{ node: 'text', text: 'inline tag' }] }
          ]
        },
        {
          node: 'element',
          tag: 'pre',
          attr: { id: 'demo', class: ['foo', 'bar'] },
          child: [{ node: 'text', text: 'foo' }]
        },
        {
          node: 'element',
          tag: 'pre',
          attr: { id: 'output', class: 'goo' },
          child: [{ node: 'text', text: 'goo' }]
        },
        {
          node: 'element',
          tag: 'input',
          attr: { id: 'execute', type: 'button', value: 'execute' }
        }
      ]
    }
  ]
}
```
