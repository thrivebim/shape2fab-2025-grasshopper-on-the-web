<!-- // Script is in some way equivalent to script.js. This is place
to define variables, methods and imports of other Vue compoennts. -->
<script setup>
// Understanding ref article: https://blog.logrocket.com/understanding-vue-refs/#:~:text=Ref%20s%20are%20Vue.,element%20in%20your%20Vue%20instance.
// When ref attribute is added to element, this element then can be referenced
// in template. It is sort of templatecement of getElementById (but better)
import { ref, onBeforeMount, computed } from "vue";
import { loadRhino } from "@/scripts/compute.js";

// Import other Vue components in order to add them to a template.
import GeometryView from "../components/BurgerGeometryView.vue"

import Toggle from "../components/Toggle.vue"
import Slider from "../components/Slider.vue"

import def from '../assets/burger_compute.gh' //import Grasshopper definition for assets

let firstSliderName = ref("Radius") //must match the Input name in your GH definition!
let firstSliderValue = ref(10) //default slider value

let secondSliderName = ref("Count") //must match the Input name in your GH definition!
let secondSliderValue = ref(10) //default slider value

let thirdSliderName = ref("Length") //must match the Input name in your GH definition!
let thirdSliderValue = ref(10) //default slider sthird


///.............................................
let path = def //path to the Grasshopper definition
let data = ref({})
let metadata = ref([])


function updateValue(newValue, parameterName) {
  console.log(parameterName)

  if (parameterName === firstSliderName.value) {
    firstSliderValue.value = newValue
  } 
  
  else if (parameterName === secondSliderName.value) {
    secondSliderValue.value = newValue
  }
  
  else if (parameterName === thirdSliderName.value) {
    thirdSliderValue.value = newValue
  }
}


// a computed ref. Vue will keep track of this and update it
const computeData = computed(() => {
  data = {
    [firstSliderName.value]: Number(firstSliderValue.value),
    [secondSliderName.value]: Number(secondSliderValue.value),
    [thirdSliderName.value]: Number(thirdSliderValue.value),
  };

  return data
})

onBeforeMount( () => {
})

</script>

<!-- Template is a HTML-based syntax that allows you to bind the rendered DOM elements
with data, objects, functions etc. -->
<template>




  <div id="app">
    <GeometryView
      v-bind:data="computeData"
      v-bind:path="path"
      v-on:updateMetadata="receiveMetedata"
      />
      
    <div class="sidebar">
      <h2> burger controls</h2>
      <Slider
      title="Levels"
      min="0"
      max="10"
      step="1"
      val="0"
    ></Slider>
    
    <Slider
      title="Width"
      min="1"
      max="10"
      step="0.1"
      val="0"
    ></Slider>

    <br>
    <h2> toppings</h2>

    
    <Toggle
    title="Mustard">
    </Toggle>
    <br>
    <Toggle
    title="Ketchup">
    </Toggle>
    <br>
    <Toggle
    title="Pickles">
    </Toggle>
    <br>
    <Toggle
    title="Onions">
    </Toggle>
    <br>

 

  
    </div>
  </div>


</template>

<!-- Style is for CSS styling -->

<style scoped>
app {
  height: 100vh;
  width: 100vw;
  overflow: hidden;
  position: relative;
  font-family: sans-serif;
}

.sidebar {
  position: fixed;
  top:100px;
  left: 20px;
  width: 300px;
  height: calc(100% - 120px);
  background-color: rgba(255, 255, 255, 0.50);
  border-radius: 12px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  padding: 1rem;
  z-index: 10;
  backdrop-filter: blur(10px); /* optional: frosted glass effect */
}

</style>