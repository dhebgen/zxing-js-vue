<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <!-- <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" /> -->
  <!-- <qr-code-scanner
    :qrbox="250"
    :fps="10"
    style="width: 500px"
    @result="onScan"
  /> -->
  <!-- <qr-scanner-zxing /> -->
  <multi-format-code-scanner-zxing />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
// import HelloWorld from './components/HelloWorld.vue';
// import qrCodeScanner from '@/components/QrScanner.vue';
// import QrScannerZxing from '@/components/QrScannerZxing.vue';
import multiFormatCodeScannerZxing from '@/components/MultiFormatReader.vue';

export default defineComponent({
  name: 'App',
  components: {
    // HelloWorld,
    // qrCodeScanner,
    // QrScannerZxing,
    multiFormatCodeScannerZxing
  },
  methods: {
    onScan(qrCodeMessage: string) {
      alert(qrCodeMessage);
    }
  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
