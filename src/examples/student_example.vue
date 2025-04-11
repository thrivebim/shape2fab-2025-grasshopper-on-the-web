
<script setup>

import { ref } from "vue";

import GeometryView from "../components/GeometryView.vue"
import Toggle from "../components/Toggle.vue"
import Slider from "../components/Slider.vue"
import Dropdown from "../components/Dropdown.vue"
import MetadataTextBox from "@/components/MetadataTextBox.vue"

import def from '../assets/your_defintion.gh' 
const path = def //path to the Grasshopper definition

const SliderName = ref("Slider") 
const SliderValue = ref(1) 

const ToggleName = ref("Toggle") 
const ToggleValue = ref(true) 

const dropdownName = ref("Dropdown")
const dropdownIndex = ref(0)
const dropdownOptions = ref([
  {label: "Option 1", value: 0},
  {label: "Option 2", value: 1},
  {label: "Option 3", value: 2}
])

let metadata = ref([])



//declare the inputs to send to compute here
let inputs = ref({

    
});


function updateValue(newValue, parameterName) {
  // Iterate over the inputs array
  for (const [key, value] of Object.entries(inputs.value)) {
    if (key == parameterName){
      inputs.value[key] = newValue
    }
  }
}

function receiveMetadata(newValue) {
  console.log(newValue)
  metadata.value = newValue
}



</script>

<!-- Template is a HTML-based syntax that allows you to bind the rendered DOM elements
with data, objects, functions etc. -->
<template>


    <div>
        <GeometryView
        d:data="inputs"
        :path="path"
        @updateMetadata="receiveMetadata"
        
        />
        
        <div class="sidebar" >

        <h2> Title </h2>
        <hr>

        <p>Some explanation of your app here </p>
        <br>

        <h2> Inputs</h2>
        <hr>

        <br>


        <Slider
            :title="SliderName"
            min="0"
            max="5"
            step="1"
            :val="SliderValue"
            @update="updateValue"
        ></Slider>

        <br>



        <Toggle
            :title="ToggleName"
            :val="ToggleValue"
            @update= "updateValue"
        ></Toggle>

        <br>


        <Dropdown 
            :title="dropdownName"
            :options="dropdownOptions" 
            :val="dropdownIndex" 
            @update="updateValue"
        ></Dropdown>

        <br>

        <h2> Metadata </h2>
        <hr>

        <MetadataTextBox :metadata="metadata"></MetadataTextBox>


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