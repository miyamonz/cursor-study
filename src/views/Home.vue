<template>
  <div class="home">
    <main-canvas />
      <ButtonGyazo />
  </div>
</template>

<script>
// @ is an alias to /src
import MainCanvas from "@/components/MainCanvas.vue";
import ButtonGyazo from "@/components/ButtonGyazo.vue";

export default {
  name: "home",
  components: {
    MainCanvas,
    ButtonGyazo
  }
};
</script>
