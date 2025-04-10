
<script setup>

import { ref, computed } from "vue";

import GeometryView from "../components/BurgerGeometryView.vue"
import Toggle from "../components/Toggle.vue"
import Slider from "../components/Slider.vue"

import def from '../assets/burger_compute.gh' 

let LevelsSliderName = ref("Levels") 
let LevelsSliderValue = ref(1) 

let MustardToggleName = ref("Mustard") 
let MustardToggleValue = ref(true) 

let OnionToggleName = ref("Onion") 
let OnionToggleValue = ref(true) 

let KetchupToggleName = ref("Ketchup") 
let KetchupToggleValue = ref(true) 

let TomatoToggleName = ref("Tomato") 
let TomatoToggleValue = ref(true) 

let CheeseToggleName = ref("Cheese") 
let CheeseToggleValue = ref(true) 

let LettuceToggleName = ref("Lettuce") 
let LettuceToggleValue = ref(true) 


let path = def //path to the Grasshopper definition
let data = ref({})

function updateValue(newValue, parameterName) {
  console.log(parameterName,newValue)

  if (parameterName === LevelsSliderName.value) {
    LevelsSliderValue.value = newValue
  } 
  
  if (parameterName === MustardToggleName.value) {
    MustardToggleValue.value = newValue
  }

  if (parameterName === OnionToggleName.value) {
    OnionToggleValue.value = newValue
  }

  if (parameterName === KetchupToggleName.value) {
    KetchupToggleValue.value = newValue
  }

  if (parameterName === TomatoToggleName.value) {
    TomatoToggleValue.value = newValue
  }

  if (parameterName === CheeseToggleName.value) {
    CheeseToggleValue.value = newValue
  }

  if (parameterName === LettuceToggleName.value) {
    LettuceToggleValue.value = newValue
  }

}


// a computed ref. Vue will keep track of this and update it
const computeData = computed(() => {
  data = {
    [LevelsSliderName.value]: Number(LevelsSliderValue.value),
    [MustardToggleName.value]: MustardToggleValue.value,
    [OnionToggleName.value]: OnionToggleValue.value,
    [KetchupToggleName.value]: KetchupToggleValue.value,
    [TomatoToggleName.value]: TomatoToggleValue.value,
    [CheeseToggleName.value]: CheeseToggleValue.value,
    [LettuceToggleName.value]: LettuceToggleValue.value,
  };

  return data
})


</script>

<!-- Template is a HTML-based syntax that allows you to bind the rendered DOM elements
with data, objects, functions etc. -->
<template>


<div>
    <GeometryView
      v-bind:data="computeData"
      v-bind:path="path"
      v-on:updateMetadata="receiveMetedata"
      />
      
    <div class="sidebar" >

      <h2> Levels</h2>
      <Slider
      :title=LevelsSliderName
      min="0"
      max="5"
      step="1"
      val="1"
      @update="updateValue"
    ></Slider>
    


    <br>
    <h2> Toppings</h2>


    <Toggle
    :title="TomatoToggleName"
    :val="TomatoToggleValue"
    @update= "updateValue"
    ></Toggle>

 
    <Toggle
    :title="OnionToggleName"
    :val="OnionToggleValue"
    @update= "updateValue"
    ></Toggle>

    <Toggle
    :title="MustardToggleName"
    :val="MustardToggleValue"
    @update= "updateValue"
    ></Toggle>


    <Toggle
    :title="KetchupToggleName"
    :val="KetchupToggleValue"
    @update= "updateValue"
    ></Toggle>

    <Toggle
    :title="CheeseToggleName"
    :val="CheeseToggleValue"
    @update= "updateValue"
    ></Toggle>


    <Toggle
    :title="LettuceToggleName"
    :val="LettuceToggleValue"
    @update= "updateValue"
    ></Toggle>


    <Toggle
    :title="MustardToggleName"
    :val="MustardToggleValue"
    @update= "updateValue"
    ></Toggle>


  </div>
  
    </div>


</template>

<style scoped>

.sidebar {
  position: fixed;
  top:100px;
  left: 20px;
  width: 300px;
  height: calc(100% - 120px);
  background-color: rgba(255, 255, 255, 0.80);
  border-radius: 12px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  padding: 1rem;
  z-index: 10;
  backdrop-filter: blur(10px); /* optional: frosted glass effect */
}

html[data-theme='dark'] .sidebar {
  background-color: rgba(0, 0, 0, 0.7) !important;
}

</style>