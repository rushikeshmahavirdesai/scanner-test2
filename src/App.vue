<template>
  <div class="w-full flex flex-col items-center justify-center h-full">
    <div v-if="data.loading">Loading....</div>
    <QuoggaReader @onDetected="onDecode" />
    <textarea name="" id="" cols="30" rows="10">{{ codeResult }}</textarea>
    <!-- <StreamBarcodeReader v-if="cart.mobileScanner" :busy="data.isAdding" @decode="onDecode" @loaded="onLoaded"></StreamBarcodeReader> -->
  </div>
</template>

<script setup>
import { ref, reactive } from "vue";

import QuoggaReader from "./components/QuoggaReader.vue";

const data = reactive({ loading: true, isAdding: false, codeResult: null });

const onLoaded = () => (data.loading = false);

const onDecode = async (text) => {
  if (data.isAdding) return false;
  data.isAdding = true;
  data.codeResult = text;
  data.isAdding = false;
};
</script>

<style scoped>
.information {
  margin-top: 100px;
}
</style>
