<script setup>
import { ref } from "vue";

// Define props coming from parent component
const props = defineProps(["title", "options"]);

const title = ref(props.title)

// Define events that will be accessible from parent component
const emits = defineEmits(["update"]);

// Value that is binded with selection option
var selectedOption = ref(0);

// Function called on change
function emitValueUpdate() {
  emits("update", selectedOption.value, title.value);
}
</script>

<template>
  <form class="definition-input">
    <label class="input-title">{{ title }} index: {{ selectedOption }} </label>

    <select
      v-model="selectedOption"
      class="dropdown"
      @change="emitValueUpdate"
>

      <option
        v-for="option in options"
        :key="option.label"
        :value="option.value"
      >
        {{ option.label }}
      </option>

     
    </select>
  </form>
</template>

<style scoped>
.dropdown {
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  background: var(--global-light) url('path_to_your_arrow_icon') no-repeat right 10px center; /* Adjust path_to_your_arrow_icon */
  border-radius: 340.074px;
  border: 2px solid  var(--global-light);
  padding: 10px 35px 10px 15px; /* Adjust padding to make room for the arrow */
  border: none;
  width: 100%;
  height: 40px;
  color: var(--custom-color);
  font-size: medium;
  cursor: pointer;
}

.dropdown:hover, .dropdown:focus {
  color: black;
  border: 2px solid var(--custom-color);
}

/* Style adjustments for options */
.dropdown option {
  color: var(--custom-color);
  border:none;
  box-shadow:none;
}
</style>
