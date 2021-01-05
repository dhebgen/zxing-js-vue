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
  BrowserQRCodeReader,
  NotFoundException,
  ChecksumException,
  FormatException
} from '@zxing/library';

const codeReader = new BrowserQRCodeReader();

export default defineComponent({
  name: 'qrCodeScannerZxing',
  data() {
    return {
      result: ''
    };
  },
  mounted() {
    this.decodeContinuously();
  },
  methods: {
    decodeContinuously() {
      codeReader.decodeFromInputVideoDeviceContinuously(
        'undefined',
        'video',
        (result, err) => {
          if (result) {
            // properly decoded qr code
            console.log('Found QR code!', result);
            this.setCode(result.getText());
          }

          if (err) {
            this.setCode('');

            // As long as this error belongs into one of the following categories
            // the code reader is going to continue as excepted. Any other error
            // will stop the decoding loop.
            //
            // Excepted Exceptions:
            //
            //  - NotFoundException
            //  - ChecksumException
            //  - FormatException

            if (err instanceof NotFoundException) {
              console.log('No QR code found.');
            }

            if (err instanceof ChecksumException) {
              console.log(
                "A code was found, but it's read value was not valid."
              );
            }

            if (err instanceof FormatException) {
              console.log('A code was found, but it was in a invalid format.');
            }
          }
        }
      );
    },
    setCode(code: string) {
      this.result = code;
    }
  }
});
</script>
<style lang="ts"></style>
