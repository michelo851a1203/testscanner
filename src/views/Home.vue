<template>
  <div class="home">
    <h2 class="px-6 py-4 rounded">{{ mainRef }}</h2>
    <Scanner @qrcode="mainFunc"></Scanner>
  </div>
</template>

<script>
// @ is an alias to /src

import { reactive, toRefs } from "vue";
import Scanner from "@/components/Scanner.vue";
export default {
  name: "Home",
  components: {
    Scanner,
  },
  setup() {
    const cluster = reactive({
      mainRef: "no Data",
      mainFunc: (qrcodeResult) => {
        cluster.mainRef = qrcodeResult;
      },
    });
    return { ...toRefs(cluster) };
  },
};
</script>
