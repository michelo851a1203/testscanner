<template>
  <div class="scanqrcode">
    <video class="border border-black w-full h-full" ref="video"></video>
  </div>
</template>

<script>
// @ is an alias to /src
import { ref, watch, onUnmounted } from "vue";
import { BrowserQRCodeReader } from "@zxing/library";

export default {
  name: "scanqrcode",
  setup(props, { emit }) {
    const codeReader = new BrowserQRCodeReader();
    const cameraRef = ref("");
    const video = ref(null);
    codeReader
      .listVideoInputDevices()
      .then((videoInputDevices) => {
        if (videoInputDevices.length === 0) {
          return;
        }
        cameraRef.value = videoInputDevices[0].deviceId;
      })
      .catch((err) => {
        console.error(err);
      });

    watch(cameraRef, (deviceId) => {
      if (deviceId === "") {
        return;
      }
      codeReader
        .decodeOnceFromVideoDevice(deviceId, video.value)
        .then((result) => {
          // console.group(`%c result`, "color:yellow");
          // console.log(result.text);
          // console.groupEnd();
          emit("qrcode", result.text);
        })
        .catch((err) => {
          console.error(err);
        });
    });

    onUnmounted(() => {
      codeReader.reset();
    });
    return { video };
  },
};
</script>
