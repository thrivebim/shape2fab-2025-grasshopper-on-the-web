<script setup>
import { ref } from "vue"
import GeometryView from "../components/MinimalisticGeometryView.vue"
import Slider from '../components/Slider.vue'
import Dropdown from "../components/Dropdown.vue"
import MetadataTextBox from "@/components/MetadataTextBox.vue"

//define path to grasshopper script
import def from "../assets/wall.gh"
const path = def


let metadata = ref([])

//Put all inputs together to send them to Rhino.Compute
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

<template>

  <div id="sidebar">

    <!-- <MetadataTextBox :metadata="metadata"></MetadataTextBox> -->
  
  </div>

  <div id="viewer">
    <!-- <GeometryView :data="inputs" :path="path" @updateMetadata="receiveMetadata"></GeometryView> -->
  </div>

</template>



<style scoped>

#sidebar {
  width: 350px;
  padding: 20px;
  flex-shrink: 0; 
}

#viewer { 
  width: 500px
}

</style>