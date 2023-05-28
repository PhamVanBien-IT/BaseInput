<script setup>
import { ref } from "vue";

import MInput from "../input/MInput.vue";

const text = ref(null);

const errorList = ref([
  {
    isStatus: false,
    labelValidate: null,
  },
  {
    isStatus: false,
    labelValidate: null,
  },
]);

function btnClick() {
  debugger;
  console.log(text.value);
  if (text.value) {
    errorList.value[0].isStatus = false;
  } else {
    errorList.value[0].isStatus = true;
    errorList.value[0].labelValidate = "Ko được để trống";
  }

  console.log(errorList);
}

function setIsValid(item) {
  errorList.value[0].isStatus = item;
  debugger;
}
</script>

<template>
  <div class="div">
    <MInput
      type="text"
      label="Giá trị"
      v-model="text"
      :isValidate="errorList[0].isStatus"
      :labelValidate="errorList[0].labelValidate"
      @isValid="
        (item) => {
          errorList[0].isStatus = item;
          console.log(errorList[0].labelValidate);
          debugger
        }
      "
    ></MInput>
    <!-- <MInput
      type="text"
      label="Tuổi"
      v-model="text.age"
      :isValidate="errorList[1].isStatus"
      :labelValidate="errorList[1].labelValidate"
      @isValid="setIsValid"
    ></MInput> -->
    <button @click="btnClick">Click</button>
  </div>
</template>
