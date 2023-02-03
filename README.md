  

# Svelte Searchable Select

  

Searchalbe and multiple select for Svelte
Npm Link: https://www.npmjs.com/package/svelte-searchable-select
Github Repository: https://github.com/ariferol01/svelte-searchable-select

  
  ![enter image description here](https://raw.githubusercontent.com/ariferol01/svelte-searchable-select/main/images/multiple-select.jpg)
  
  

## Installation

  

Available on NPM

  

```bash

$ npm i svelte-searchable-select

```

  

## How to use

  

```javascript

<script>

  

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

  

For binding items array to fields (bind:fields)

```javascript

  

<Select

bind:result={selectedCountries}

bind:fields={countries}

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