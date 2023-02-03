# svelte-searchable-select
svelte-searchable-select is a vanilla javascript component which will work in any frontend framework. You can install from npm like this:

```text
npm install --save svelte-searchable-select
```

#### Usage: Javascript (assumes es module) 
```javascript
import Select from 'svelte-searchable-select'

let select = new Select({target:document.body, props: { fields: 'Init Value' });
select.fields = 'Updated Value'; 
// Other props: text, multiple, className, result, selectedsClass, placeholderText
```

The "target" is where the component is created. Here it is added to the html body with "document.body", but it could also be document.getElementById('id-of-html-element'). 

You initialize properties with "props" and you can change the prop values by just assigning the props to new values - this will be updated in the UI. 

#### Usage: Legacy Javascript
Below you can see how to use the component with vanilla js.
```html
...
<head>
  ...
  <script src="https://unpkg.com/svelte-searchable-select@0.0.1/index.js"></script>
</head>
<body>
  <script>
    let select = new Select({target:document.body})
  </script>
</body>
```

#### Usage: Web Component (aka. Custom Element)
You can use it as a web component.
```html
<head>
  <script src="https://unpkg.com/svelte-searchable-select@0.0.1/index.js"></script>
</head>
<body>
  <name-of-ce fields="Init Value" />    
</body>
```
WARNING: The author of the component needs to add <svelte:options tag="name-of-ce"/>.
#### Svelte Component
```html
<script>
  import Select from 'svelte-searchable-select';
</script>
<Select/>
```

#### Pelte
This component was created by [pelte](https://www.npmjs.com/package/publish-svelte) (aka publish-svelte)