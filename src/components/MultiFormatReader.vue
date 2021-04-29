<template>
  <div>
    <div>
      <video id="video" width="300" height="300" />
    </div>
    <label>Result: </label>
    <pre>
      <code id="result">{{result}}</code>
    </pre>
  </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import {
  BrowserMultiFormatOneDReader,
  BrowserQRCodeReader
} from '@zxing/browser';

// const codeReader = new BrowserQRCodeReader();

export default defineComponent({
  name: 'multiFormatCodeScannerZxing',
  data() {
    return {
      result: ''
    };
  },
  mounted() {
    this.decodeContinuously();
  },
  methods: {
    async decodeContinuously() {
      // codeReader.listVideoInputDevices();
      const previewElem = document.querySelector(
        '#test-area-qr-code-webcam > video'
      );

      const videoInputDevices = await BrowserMultiFormatOneDReader.listVideoInputDevices();

      // choose your media device (webcam, frontal camera, back camera, etc.)
      const selectedDeviceId = videoInputDevices[0].deviceId;

      const codeReader = new BrowserMultiFormatOneDReader();
      // const codeReader = new BrowserQRCodeReader();

      // you can use the controls to stop() the scan or switchTorch() if available
      const controls = await codeReader.decodeFromVideoDevice(
        selectedDeviceId,
        'video',
        (result, error, controls) => {
          // use the result and error values to choose your actions
          // you can also use controls API in this scope like the controls
          // returned from the method.
          console.log('Started scanning!');
          if (error) {
            console.log(error);
          }
          if (result) {
            // properly decoded qr code
            console.log('Found QR code!', result);
            const text = result.getText();
            if (text !== '') {
              this.setCode(text);
            }
          }
        }
      );
      // stops scanning after 60 seconds
      /* setTimeout(() => {
        controls.stop();
        console.log('stopped scanning');
      }, 60000) */
    },
    setCode(code: string) {
      this.result = code;
    }
  }
});
</script>
<style lang="ts"></style>
