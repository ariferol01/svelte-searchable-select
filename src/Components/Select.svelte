<script>
	import { fade } from 'svelte/transition';
  import {onMount} from "svelte"
  export let 
  fields, 
  text, 
  multiple = true,
  className, 
  result,
  selectedsClass,
  placeholderText
  
  let selected_names = [];
  let selector_area;

  if (typeof text == 'object') {
    text = text[0][text[1]];
  }

  if (result.length > 0) {
    for (let i = 0; i < result.length; i++) {
      result[i].this_selected = true;
      selected_names.push(result[i][text]);
    }
  }

  for (let i = 0; i < fields.length; i++) {
    fields[i].this_selected = (selected_names.includes(fields[i][text])) ? true : false ;
    fields.filtered_list = false;
  }

  let focused;
  let placeholder = (result.length > 0) ? '' : '<span class="placeholderText">'+placeholderText+'</span>' ;
  $:selector = [placeholder];
  let selecteds;

  function getResult(){
    result = false;
    result = fields.filter((item) => {
      return item.this_selected;
    });
    return result;
  }

  $:if(result){
    result = getResult();
  }
  
  function start_selecting(){
    placeholder = '';
    setTimeout(() => {
      focused = true;
    }, 100);
  }

  function stop_selecting(){
    setTimeout(() => {
      focused = false;
    }, 80);
  }


  function select_field(index){
    selector_area.focus();
    placeholder = '';
    let field = fields[index];
    let exists = result.filter((elem) => {
      return (elem[text] == field[text]);
    }).length > 0;
    
    if (!exists) {
      if (!multiple) {
        fields.forEach((item, i) => {
          fields[i].this_selected = false;
        });
      }
      fields[index].this_selected = true;
    }

    getResult()
  }

  function unselect_filed(field){
    selector_area.focus();
    fields.map((item, i) => {
      if (item[text] == field[text]) {
        fields[i].this_selected = false;
      }
    });
    getResult()
  }

  function filter_select(event){
    let filteText = event.target.innerText;
    
    fields.forEach((item, i) => {
      let vall = filteText.toLowerCase().toString();
      if (item.this_selected !== true) {
        if (filteText.length > 0) {
          fields[i].filtered_list = (item[text].toLowerCase().toString().split(vall).length > 1) ? false : true ;
        }else{
          fields[i].filtered_list = false;
        }
        
      }
    });

  }

  

</script>

<div id="svSelectCont" class="sv-select-cont" in:fade>
  <div class="sv-editorcont {className}">
      <div class="selecteds-cont">
        {#if result}
          {#each result as field}
            <span class="selected-label-elem {selectedsClass}" class:selected={field.this_selected}>
              <span class="selected-text">{field[text]}</span> <a class="remove-selected" href={null} on:click={() => {unselect_filed(field)}}>x</a>
            </span>
          {/each}
        {/if}
        <div
    bind:this={selector_area}
    class="selector-area"
    contenteditable="true"
    on:focus={() => {start_selecting()}}
    on:blur={stop_selecting}
    on:keyup={event => {filter_select(event)}}
    >
    {@html placeholder}
  </div>
      </div>
    
  </div>

  <div class="w-100 field-list-cont" class:active={focused}>
    <div class="field-list active">
      {#each fields as field, index}
        <a href={null} class="sv-listed-elem-{text}" on:click={() => {select_field(index)}} class:selected={!field.this_selected} class:filtered={field.filtered_list} >{field[text]}</a>
      {/each}
    </div>
  </div>

</div>


<style>
  .sv-select-cont{
    position: relative;
    width: 100%;
    display: block;
  }
  .placeholderText{
    font-size: .8rem;
  }
  .field-list{
    position: absolute;
    max-height: 400px;
    left:0;
    top:100%;
    width: 100%;
    min-width: 300px;
    overflow-y: auto;
    display: none;
    z-index: 9;
  }
  .field-list a{
    display:none;
    padding: .5rem;
    font-size: .95rem;
    border:0px;
    outline: none;
    border-bottom: 1px solid rgba(0,0,0, .05);
    background-color: #fff;
    width: 100%;
    text-align: left;
  }
  .field-list a:focus{
    outline: none;
    border: 0px;
  }
  .field-list a.selected, .field-list a.filtered{
    display:block;
  }

  .field-list a.filtered.selected{
    display:none;
  }

  .field-list a:hover{
    background-color: rgb(218, 218, 218);
  }
  .field-list.active{
    display:block;
  }
  .selected-label-elem{
    position: relative;
    margin-right: 1rem;
    display: none;
    align-items: center;
    justify-content: center;
  }

  .selected-label-elem.selected{
    display:inline-flex;
  }
  .selector-area{
    display: inline;
    flex-wrap: nowrap;
    width: auto;
    min-width: 100px;
    padding: 0px 5px;
  }

  .selector-area:focus{
    outline: 0px!important;
    border: 0px!important;
  }

  .selected-text{
    margin-right: .4rem;
  }

  .remove-selected{
    display: inline-flex;
    align-items: center;
    justify-content: center;
    background-color: red;
    color: #fff;
    font-size: .7rem;
    padding: 0.2rem;
    border-radius: 50%;
    width: 1rem;
    height: 1rem;
  }

  .sv-editorcont{
    display:flex;
    flex-wrap: nowrap;
    align-items: center;
    justify-content: flex-start;
    min-width: 100px;
    height:100%;
    position: relative;
    z-index: 2;
  }

  .selecteds-cont{
    display: flex;
    flex-wrap: wrap;
    align-items: center;
  }
  .field-list-cont{
    position: relative;
    display:none;
    z-index:9;
  }
  .field-list-cont.active{
    display:block;
  }
</style>