<template>
  <canvas 
    :width="width" :height="height" ref="canvas"
    ></canvas>
</template>
<script>
export default {
  props: ["width", "height", "penWidth"],
  computed: {
    context() {
      return this.$refs.canvas.getContext("2d");
    }
  },
  methods: {
    drawCursor(x, y) {
      const ctx = this.context;
      ctx.clearRect(0, 0, this.width, this.height);
      ctx.beginPath();
      ctx.lineCap = "round";
      ctx.lineWidth = 1;
      ctx.strokeStyle = "#555555";
      ctx.arc(x, y, this.penWidth / 2, 0, Math.PI * 2, false);
      ctx.stroke();
    }
  }
};
</script>
