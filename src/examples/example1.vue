<template>

  <div>
    <div id="sidebar">

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

    <Toggle
    title="Lettuce">
    </Toggle>
    <br>
    <Toggle
    title="Tomato">
    </Toggle>

    <br>
    <Toggle
    title="Cheese">
    </Toggle>


    </div>

    <div id="viewer">


 

      
    </div>
</div>


</template>

<script setup>
import Slider from "../components/Slider.vue";
import Toggle from "../components/Toggle.vue";



</script>

<style scoped>
#sidebar {
  width: 310px;
  padding: 20px;
  flex-shrink: 0;
}

#viewer {
  width: 100%;
  margin: 20px;
}
</style>
