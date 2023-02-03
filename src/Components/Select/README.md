
# Svelte Searchable Select

Searchalbe and multiple select for Svelte




## Installation

Available on NPM

```bash
  $ npm i svelte-searchable-select
```

  
## How to use

```javascript
<script>
export let openside;

import Select from "svelte-searchable-select";

let countries = [
  {
    name: 'United States',
    iso_3: 'USA',
    phone_code: '+1'
  },
  
  {
    name: 'United Kingdom',
    iso_3: 'GBR',
    phone_code: '+44'
  },
  
  {
    name: 'Türkiye',
    iso_3: 'TUR',
    phone_code: '+90'
  },

];

let selectedCountries = [];

$:console.log('Selected Countries: ', selectedCountries);

</script>

  <Select 
  bind:result={selectedCountries}
  fields={countries}
  text={'name'}
  multiple={true}
  className={'form-control'} 
  selectedsClass={"rounded p-2"}
  placeholderText={"Select Country"}
  />
  
```



### For selected default fields

```javascript
let selectedCountries = [countries[1]];
```


