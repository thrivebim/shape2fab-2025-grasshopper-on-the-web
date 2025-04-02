<script setup>
import { ref, onMounted, watch } from "vue";

const props = defineProps(["title", "min", "max", "step", "val"]);
const emits = defineEmits(["update"]);

var sliderValue = ref(props.val);

function emitValueUpdate() {
  emits("update", sliderValue.value, title.value);
}

const updateSlider = () => {
  if (!rangeInput.value) return;
  const val =
    ((sliderValue.value - props.min) / (props.max - props.min)) * 100;
  rangeInput.value.style.setProperty("--value", `${val}%`);
};

onMounted(() => {
  const rangeInput = document.querySelector(".modern-range");
  const val =
    ((rangeInput.value - rangeInput.min) / (rangeInput.max - rangeInput.min)) *
    100;
  rangeInput.style.setProperty("--value", `${val}%`);
});
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
