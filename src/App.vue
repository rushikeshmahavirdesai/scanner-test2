<template>
  <div class="w-full flex flex-col items-center justify-center h-full">
    <QuoggaReader :onDetected="onDecode" />
    <textarea name="" id="" cols="30" rows="10">{{ data.codeResult }}</textarea>
    <!-- <StreamBarcodeReader v-if="cart.mobileScanner" :busy="data.isAdding" @decode="onDecode" @loaded="onLoaded"></StreamBarcodeReader> -->
  </div>
</template>

<script setup>
import { ref, reactive } from "vue";

import QuoggaReader from "./components/QuoggaReader.vue";

const data = reactive({ loading: true, isAdding: false, codeResult: null });

const onLoaded = () => (data.loading = false);

const onDecode = async (text) => {
  alert("deteched");
  data.codeResult = text;
};
</script>

<style scoped>
.information {
  margin-top: 100px;
}
</style>
