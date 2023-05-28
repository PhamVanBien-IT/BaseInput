<template>
  <div class="base-input">
    <div class="label-input">
      {{ label }} <sup style="color: red">{{ required }}</sup>
    </div>
    <div class="input-container">
      <input
        :type="typeInput"
        v-model="valueInput"
        class="text-form"
        :class="{ 'bd-red': isValid }"
        @input="hanldeBlurInput"
      />
    </div>
    <div class="text-validate" v-if="isValid">
      {{ valid }}
    </div>
  </div>
</template>
<script setup>
import { computed, onMounted, onUpdated, ref, watch } from "vue";

const emit = defineEmits(["update:modelValue"]);

const props = defineProps([
  "class",
  "type",
  "modelValue",
  "labelValidate",
  "label",
  "isValidate",
]);

const valueInput = ref(props.modelValue);

let valid = ref(null);
let isValid = ref(false);

// let isValid = ref(false);

function hanldeBlurInput() {
  if (valueInput.value) {
    if(valueInput.value != "")
    isValid.value = false;
  } else {
    isValid.value = true;
  }

  emit("isValid", isValid.value);

  debugger;
}

onUpdated(() => {
  valid.value = props.labelValidate;
  isValid.value = props.isValidate;

  console.log(isValid.value, valueInput.value);
});

watch(
  valueInput,
  (newValue) => {
    emit("update:modelValue", newValue);
  },
  { deep: true }
);
</script>

<style scoped>
.bd-red {
  border: 1px solid red;
}
</style>;
