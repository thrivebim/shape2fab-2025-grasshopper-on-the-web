<script setup>
import { ref, onMounted, watch } from "vue";

const props = defineProps(["title", "min", "max", "step", "val"]);
const emits = defineEmits(["update"]);

const title = ref(props.title);
const sliderValue = ref(props.val);
const rangeInput = ref(null); // Reference to the input element

function emitValueUpdate() {
  emits("update", sliderValue.value, title.value);
}

const updateSlider = () => {
  if (!rangeInput.value) return;
  const val =
    ((sliderValue.value - props.min) / (props.max - props.min)) * 100;
  rangeInput.value.style.setProperty("--value", `${val}%`);
};

// Update the slider style when value changes
watch(sliderValue, updateSlider);
onMounted(updateSlider);
</script>

<template>
  <div>
    <form class="definition-input">
      <label class="input-title">{{ title }}: {{ sliderValue }}</label>
      <input
        ref="rangeInput"
        type="range"
        class="modern-range"
        :min="min"
        :max="max"
        :step="step"
        v-model="sliderValue"
        @input="updateSlider"
        @mouseup="emitValueUpdate"
      />
    </form>
  </div>
</template>

<style scoped></style>
