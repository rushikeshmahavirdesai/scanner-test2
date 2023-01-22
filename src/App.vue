<template>
  <video id="stream" style="width: 100vw; height: 100vh" />
</template>

<script>
export default {
  name: "stream-barcode-reader",
  props: {},
  data() {
    return {
      barcodeDt: "hhh",
    };
  },

  mounted() {
    (async () => {
      const stream = await navigator.mediaDevices.getUserMedia({
        video: {
          facingMode: {
            ideal: "environment",
          },
        },
        audio: false,
      });
      const videoEl = document.querySelector("#stream");
      videoEl.srcObject = stream;
      await videoEl.play();
      debugger;
      const barcodeDetector = new BarcodeDetector({ formats: ["qr_code"] });
      window.setInterval(async () => {
        const barcodes = await barcodeDetector.detect(videoEl);
        if (barcodes.length <= 0) return;
        alert(barcodes.map((barcode) => barcode.rawValue));
      }, 1000);
    })();
  },

  // beforeUnmount() {
  //   this.codeReader.reset();
  // },

  // methods: {
  //   onScanSuccess(decodedText, decodedResult) {
  //     this.barcodeDt = decodedText;
  //     this.$emit("result", decodedText, decodedResult);
  //   },
  // },
};
</script>
