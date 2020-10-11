<template>
  <div class="home">
    <Scanner></Scanner>
  </div>
</template>

<script>
// @ is an alias to /src

import Scanner from "@/components/Scanner.vue";

export default {
  name: "Home",
  components: {
    Scanner,
  },
};
</script>
