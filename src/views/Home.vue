<template>
  <div class="home">
    <main-canvas />
  </div>
</template>

<script>
// @ is an alias to /src
import MainCanvas from "@/components/MainCanvas.vue";

export default {
  name: "home",
  components: {
    MainCanvas
  }
};
</script>
