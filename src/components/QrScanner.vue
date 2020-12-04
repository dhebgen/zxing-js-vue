<template>
  <h1>QR Code Scanner Showcase</h1>
  <div id="qr-code-full-region"></div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
// import Html5QrcodeScanner from 'html5-qrcode/minified/html5-qrcode.min';
const Html5QrcodeScanner = require('html5-qrcode/minified/html5-qrcode.min');
export default defineComponent({
  name: 'qrCodeScanner',
  props: {
    qrbox: {
      type: Number,
      default: 250
    },
    fps: {
      type: Number,
      default: 10
    }
  },
  mounted() {
    const qrCodeScript = document.createElement('script');
    qrCodeScript.setAttribute(
      'src',
      'https://unpkg.com/html5-qrcode/minified/html5-qrcode.min.js'
    );
    document.head.appendChild(qrCodeScript);
    const config = {
      fps: this.fps,
      qrbox: this.qrbox
    };
    const html5QrcodeScanner = new Html5QrcodeScanner(
      'qr-code-full-region',
      config
    );
    html5QrcodeScanner.render(this.onScanSuccess);
  },
  methods: {
    onScanSuccess(qrCodeMessage: string) {
      this.$emit('result', qrCodeMessage);
    }
  }
});
</script>

<style></style>
